- app调用web页面loading动画

	base.addLoading();
- app删除web页面loading动画

	base.removeLoading();
- app调用web页面下载进度条,参数arg是1到100之间的数字

	progress(arg);
- app调用web页面下载失败对话框

	upload_fail();
- web页面调用app下载静态文件

	window.native.upload();
- 原生应用进入每一个页面调用一下web端的render方法，并传参

	render(json);

- web端跳转页面调用原生的native.page_to方法，第一个参数是跳转页面标识，第二个参数可省略，当存在时，是纯字符串或json格式。

	native.page_to({
        link: content,(必须参数)
        task_id: task_id,（可选参数）
    });

- web端调用原生的Facebook分享，第一个参数是分享内容，第二个参数是回调函数名称

	native.share_facebook({
        content: content,
        callback: callback_name
    });

- web端调用原生的Facebook登录，第一个参数是回调函数名称

	native.login_facebook({
        callback: callback_name
    });

- web端调用原生的剪切板操作，第一个参数是复制内容，第二个参数是回调函数名称

	native.copy({
        content: content,
        callback: callback_name
    });

- （其他遇到再加）


登录接口
0：    @"status”:@(0),@“msg”:@“失败信息”
1：    @"status":@(1),@"msg":@"成功"
2：    @"status”:@(2),@“msg”:@“用户返回”
3：    @"status”:@(3),@“msg”:@“已登录”
