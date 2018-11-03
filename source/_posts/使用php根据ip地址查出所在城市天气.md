title: 使用php根据ip地址查出所在城市天气
date: 2016-07-07 20:59:10
categories: php
---
###使用PHP根据ip地址查出所在城市天气
php code 
```bash
    <?php
     
	    	header("Content-type:text/html;charset=utf8");
	    
	    /**
	     * 本地ip获取函数 
	     * 
	     * @return   string
	     * @author   Matthew
	     * @copyright 2016-07-06
	     */
	    function get_client_ip(){
	    if ($_SERVER['REMOTE_ADDR']) {
	     $cip = $_SERVER['REMOTE_ADDR'];
	    } elseif (getenv("REMOTE_ADDR")) {
	     $cip = getenv("REMOTE_ADDR");
	    } elseif (getenv("HTTP_CLIENT_IP")) {
	     $cip = getenv("HTTP_CLIENT_IP");
	    } else {
	     $cip = "unknown";
	    }
	    return $cip;
	    }
	    
	    
	    $local_ip = get_client_ip();//获取本地ip
	    
	    /**
	     * 本地ip对应城市名称函数
	     * @param string $ip
	     * @author Matthew
	     * @copyright 2016-07-06
	     */
	    function GetIpLookup($ip){  
	    if(empty($ip)){  
	    $ip = get_client_ip();  
	    }  
	    /*使用新浪的 api 根据ip来查询城市*/
	    $res = @file_get_contents('http://int.dpool.sina.com.cn/iplookup/iplookup.php?format=js&ip='.$ip);  
	    if(empty($res)){
	    return false; 
	    }  
	    $jsonMatches = array(); 
	    
	    // . 匹配除"\n"以外的任何单个字符
	    // + 匹配前面的子表达式一次或多次
	    // ? 匹配前面的子表达式 0次或 1次 
	    //var_dump($res);
	    /*从得到的数据中取出json格式部分,并将其赋值给数组 $jsonMatches[0]*/
	    preg_match('#\{.+?\}#', $res, $jsonMatches);  
	    
	    if(!isset($jsonMatches[0])){ 
	    return false; 
	    }
	    
	    /*接受一个 JSON 格式的字符串并且把它转换为 PHP 变量，true表示返回 Array*/
	    $json = json_decode($jsonMatches[0], true);
	    /*
	    if(isset($json['ret']) && $json['ret'] == 1){  
	    //$json['ip'] = $ip;  
	    unset($json['ret']);  
	    }else{  
	    return false;  
	    }  
	    */
	    return $json;  
	    }  
	    
	    $location = GetIpLookup($local_ip);
	    //echo "<pre>";
	    //print_r($location);
	    $city = $location["city"];
	    //echo "</pre>";
	    
	    /*初始化一个cURL会话*/
	    /*根据地址获取天气api来源：http://apistore.baidu.com/apiworks/servicedetail/478.html*/
	    $ch = curl_init();
	    	$url = "http://apis.baidu.com/heweather/weather/free?city=$city";
	    $header = array(
	    //需填写手机号获取
	    'apikey: c4b3604b699cf6f8acab3f08ac769cb3',
	    );
	    
	    // 添加apikey到header
	    // CURLOPT_HTTPHEADER   应传入数组类型
	    curl_setopt($ch, CURLOPT_HTTPHEADER  , $header);
	    
	    //CURLOPT_RETURNTRANSFER将 curl_exec() 获取的信息以文件流的形式返回，而不是直接输出。
	    //第三个参数应传入 bool类型
	    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
	    
	    // 执行HTTP请求
	    // CURLOPT_URL   需要获取的URL地址，也可以在 curl_init() 函数中设置。 
	    // 第三个参数应传入字符串类型
	    curl_setopt($ch , CURLOPT_URL , $url);
	    
	    //执行给定的cURL会话
	    $res = curl_exec($ch);
	    
	    $arr = json_decode($res,true);
	    echo "<pre  style='font-size:12px;margin:13px 5px 5px 25px;font-family: Arial, Helvetica, sans-serif;'>";
	    echo $arr["HeWeather data service 3.0"][0]["basic"]["city"]."   ".$arr["HeWeather data service 3.0"][0]["basic"]["cnty"];
	    echo "<br>";
	    echo "白天：".$arr["HeWeather data service 3.0"][0]["daily_forecast"][0]["cond"]["txt_d"]."<br>";
	    echo "夜晚：".$arr["HeWeather data service 3.0"][0]["daily_forecast"][0]["cond"]["txt_n"]."<br>";
	    echo "气温：".$arr["HeWeather data service 3.0"][0]["daily_forecast"][0]["tmp"]["min"]."℃ ～ ".$arr["HeWeather data service 3.0"][0]["daily_forecast"][0]["tmp"]["max"]."℃<br>";
	    echo "更新时间：".$arr["HeWeather data service 3.0"][0]["basic"]["update"]["loc"]."<br>";
	    echo "</pre>";
    
    ?>
```