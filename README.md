# shopex-b2b2c-doc-spider
商派b2b2c文档爬虫


php代码如下：

```
<?php


$url = ('http://club.ec-os.net/doc/b2b2c-dev/100.preface/README.md');

$c = trim(file_get_contents($url));




preg_match_all('!<li><a href="(.*\.md)">.*</a>!',$c,$m);



foreach ($m[1] as $k => $v) {

// if ($v != '700.operator/100.deploy/500.setup.md') continue;

    $filepath = __DIR__.'/'.$v;

    $pi = pathinfo($filepath);
    @mkdir($pi['dirname'],0777,true);
    
    $targetUrl = 'http://club.ec-os.net/doc/b2b2c-dev/'.$v;
    $cc =  trim(file_get_contents($targetUrl));

    if (!file_exists($filepath)) {
        file_put_contents($filepath, $cc);
    }

    echo $v . PHP_EOL;


	
    preg_match_all('!<img src=\'images/(.*)\'!',$cc,$mm);


    foreach($mm[1] as $kk => $vv) {
        $imageUrl = 'http://club.ec-os.net/doc/b2b2c-dev/'.substr($v,0,strrpos($v,'/')).'/images/'.$vv;

echo 'imageUrl '.$imageUrl.PHP_EOL;

        $image = file_get_contents($imageUrl);
        $imagepath = __DIR__.'/'.substr($v,0,strrpos($v,'/')).'/images/'.$vv;

echo 'imagepath '.$imagepath.PHP_EOL;

        $imgpi = pathinfo($imagepath);
        @mkdir($imgpi['dirname'],0777,true);

        file_put_contents($imagepath, $image);

        if ('700.operator/100.deploy' == strrpos($v,'/')) {
        	echo $imageUrl.PHP_EOL;
        	echo $imagepath.PHP_EOL;
        }

    }

    preg_match_all('!<img src="images/(.*)"!',$cc,$mm);
    foreach($mm[1] as $kk => $vv) {
        $imageUrl = 'http://club.ec-os.net/doc/b2b2c-dev/'.substr($v,0,strrpos($v,'/')).'/images/'.$vv;
echo 'imageUrl '.$imageUrl.PHP_EOL;

        $image = file_get_contents($imageUrl);
        $imagepath = __DIR__.'/'.substr($v,0,strrpos($v,'/')).'/images/'.$vv;

echo 'imagepath '.$imagepath.PHP_EOL;
        $imgpi = pathinfo($imagepath);
        @mkdir($imgpi['dirname'],0777,true);

        file_put_contents($imagepath, $image);

        if ('700.operator/100.deploy' == strrpos($v,'/')) {
        	echo $imageUrl.PHP_EOL;
        	echo $imagepath.PHP_EOL;
        }

    }


   

}









```

