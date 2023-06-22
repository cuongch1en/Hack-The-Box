# Juggling facts
## Steps

1. The challange's name is `Juggling .. `, I think it is the type of juggling vulnerability.
2. Check source, we have `$router->new('POST','/api/getfacts', 'IndexController@getfacts');` in `index.php`

A snippet in `IndexController.php`
```
 public function getfacts($router)
 {
     $jsondata = json_decode(file_get_contents('php://input'), true);

     if ( empty($jsondata) || !array_key_exists('type', $jsondata))
     {
         return $router->jsonify(['message' => 'Insufficient parameters!']);
     }

     if ($jsondata['type'] === 'secrets' && $_SERVER['REMOTE_ADDR'] !== '127.0.0.1')
     {
         return $router->jsonify(['message' => 'Currently this type can be only accessed through localhost!']);
     }

     switch ($jsondata['type'])
     {
         case 'secrets':
             return $router->jsonify([
                 'facts' => $this->facts->get_facts('secrets')
             ]);

         case 'spooky':
             return $router->jsonify([
                 'facts' => $this->facts->get_facts('spooky')
             ]);
         
         case 'not_spooky':
             return $router->jsonify([
                 'facts' => $this->facts->get_facts('not_spooky')
             ]);
         
         default:
             return $router->jsonify([
                 'message' => 'Invalid type!'
             ]);
     }
 }
```
3. We try ` { "type":"secrets" }`:

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/e620a032-f450-48c6-994c-e5c97c275b3c)


4. How the above snippet works? : checks input, compares `type` parameter and `if` type === secrets && REMOTE_ADDR !== 127.0.0.1 return a message:

`else` return `switch case` (it is the vulnerability)

`switch ($jsondata['type'])`  is same as  `$jsondata['type'] == ???`

5. It is a loose comparison, [document about it](https://www.php.net/manual/en/types.comparisons.php).

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/f8afa4a9-233c-4c29-9947-2efa9188308e)


We can understand `True` == `any string` retrurn `true`.

6. Final payload `{"type":True}`

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/8c746e90-fdcb-42bf-ad54-5a1c9b6e8b04)

