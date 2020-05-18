---
layout: post
title: "laravel phpexcel功能 操作excel表格"
date: 2019-11-06 
description: "laravel"

tag:laravel
---   



#### lavavel 使用 phpexcel功能

1.安装

使用命令行用 composer 安装 maatwebsite/excel

##### 执行以下代码

```
composer require maatwebsite/excel
```

![img](https://img2018.cnblogs.com/i-beta/1314204/201911/1314204-20191121174834570-79328399.png)

 Package manifest generated successfully. 表示安装成功



##### 打开config/app.php 文件

添加以下代码

```
'providers' => [
      
     Maatwebsite\Excel\ExcelServiceProvider::class,
]
```

```
 'aliases' => [

'Excel' => Maatwebsite\Excel\Facades\Excel::class,

],
```



##### 发布配置，请运行vendor publish 命令：

```
php artisan vendor:publish
```

或者

```
php artisan vendor:publish --provider="Maatwebsite\Excel\ExcelServiceProvider"
```

将会自动创建一个新配置文件config/excel.php

#### 3. 用法

先创建导出类，以导出用户为例

```
php artisan make:export UserExport
```

以下为导出类代码（UserExport.php）

app/Exports/UserExport.php

```
<?php

namespace App\Exports;

use Maatwebsite\Excel\Concerns\FromCollection;

class UserExport implements FromCollection
{
    private $row;
    private $data;

    public function __construct($row,$data)
    {
        $this->row = $row;
        $this->data = $data;
    }

    public function collection()
    {
        $row = $this->row;
        $data = $this->data;

        //设置表头
        foreach ($row[0] as $key => $value) {
            $key_arr[] = $key;
        }

        //输入数据
        foreach ($data as $key => &$value) {
            $js = [];
            for ($i=0; $i < count($key_arr); $i++) {
                $js = array_merge($js,[ $key_arr[$i] => $value[ $key_arr[$i] ] ]);
            }
            array_push($row, $js);
            unset($val);
        }
        return collect($row);
    }
}
```

#### 4.调用方法， 导出文件（UserController.php）

```
<?php

namespace App\Http\Controllers\Admin;

use Maatwebsite\Excel\Facades\Excel;
use App\Exports\UserExport;
use App\Models\User as userModel;


class UserController extends Controller
{
    /**
     * 用户列表导出
     * @param Request $request
     */
    public function user_export(Request $request){

　　　　//设置表头
        $row = [[
            "id"=>'ID',
            "nickname"=>'用户昵称',
            "gender_text"=>'性别',
            "mobile"=>'手机号',
            "addtime"=>'创建时间  '
        ]];

       //数据$list=[
            0=>[
                "id"=>'1',
                "nickname"=>'张三',
                "gender_text"=>'男',
                "mobile"=>'18812345678',
                "addtime"=>'2019-11-21  '
            ],
            2=>[
                "id"=>'2',
                "nickname"=>'李四',
                "gender_text"=>'女',
                "mobile"=>'18812349999',
                "addtime"=>'2019-11-21  '
            ]
        ];
　　
　　　　//执行导出
        return Excel::download(new UserExport($row,$list), date('Y:m:d ') . '用户列表.xls'); 
  } }

```

导出完成

![img](https://img2018.cnblogs.com/i-beta/1314204/201911/1314204-20191121180608619-984392575.png)