> Call API:-
```
_curl(array("name"=>"dinesh"),"post")
```
> Using below function, we can upload file or submit form data
```
function _curl($data,$method)
{      
  $headers = [
    "Devicetokens: your device-token",
    "Devicetype: website or mobile",
    "Language: en or fr or etc",
    "Content-Type:multipart/form-data"
  ];
  $url="www.domain.com/signIn";
  $handle = curl_init($url);
  if(isset($_FILES) && sizeof($_FILES)>0 && !empty($_FILES[array_keys($_FILES)[0]]["tmp_name"]))
  {
    $fileData = [
    'filename' => new \CurlFile($_FILES[array_keys($_FILES)[0]]["tmp_name"], $_FILES[array_keys($_FILES)[0]]["type"], $_FILES[array_keys($_FILES)[0]]["name"])
    ];
    $data=array_merge($data,$fileData);
  }  
  curl_setopt($handle, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
  curl_setopt($handle, CURLOPT_USERPWD, 'username:password');
  curl_setopt($handle, CURLOPT_RETURNTRANSFER, true);
  curl_setopt($handle, CURLOPT_POST, true);
  curl_setopt($handle, CURLOPT_POSTFIELDS, $data);
  curl_setopt($handle, CURLOPT_HTTPHEADER, $headers);
  $result=curl_exec($handle);
  curl_close($handle);
  return $result;
}  
```