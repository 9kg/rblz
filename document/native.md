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

- web端调用原生的剪切板操作，第一个参数是复制内容，第二个参数是回调函数名称

	native.copy({
        content: content,
        callback: callback_name
    });

- （其他遇到再加）
