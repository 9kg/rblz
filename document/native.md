`所有的原生对web的回调函数（callback）的传参必须是json对象(字典)格式。`

`所有的对原生的请求如果数据异常且存在callback,那么原生需要callback_name({errcode:0});errcode: 0:网络异常，1:请求失败，2：服务端给原生的status不为10时，同时原生需要把服务端的msg带过来callback_name({errcode:2，msg:msg});。`

- `1`.app调用web页面loading动画 `2`.app取消web页面loading动画

	base.addLoading();

	base.removeLoading();

---

- web端每进入一个页面或刷新当前页面会调用原生应用的render方法获取数据，(`callback`是回调函数名称)

	native.render({
		callback: callback_name
	});

	**3个记录页（redeem_records,task_friend,task_records）的数据原先是[{},{}...],现在调整为{data:[{},{}...]}**
	这三个记录页需要上拉加载，会额外传2个参数

	`cur_page`：当前页，默认从1开始

	`page_size`：每一页显示记录数（如果后台返回记录数不足，我会认为是最后一页，禁止用户下拉加载。）

	**参考回调数据见统计目录下`data.md`**

---

- web端跳转页面调用原生的native.page_to方法，(`link`是跳转页面标识，`title`是跳转页面标题，`task_id`是任务id(只在任务列表页跳任务详情页用到),有其他参数再加

	native.page_to({
		link: content,(必须参数)
        title: title,(必须参数)
        task_id: task_id（可选参数）
	});

---

- web端调用原生的Facebook登录  (`callback`是回调函数名称）

	native.login_facebook({
        callback: callback_name
    });

    callback_name({status:0});

    status: 0:登录失败，1:登录成功，2：登录取消;

---

- web端调用原生的Facebook分享（`content`是分享内容，`callback`是回调函数名称）

	native.share_facebook({
        content: content,
        callback: callback_name
    });

    callback_name({status:0});

    status: 0:分享失败，1:分享成功，2：分享取消;

---

- web端调用原生的剪切板操作（`content`是复制内容，`callback`是回调函数名称）

	native.copy({
        content: content,
        callback: callback_name
    });

    callback_name({status:0});

    status: 0:复制失败，1:复制成功;

---

- 任务详情开始任务 (`callback`是回调函数名称）

	native.task_install({
		callback: callback_name
	});

    callback_name({status:1});

    status: 1:成功;

---

- <del>记录列表页的刷新	（**这个废弃**）</del>

	<del>
	native.refresh({
		callback: callback_name
	});
	</del>

---


- 礼品卡兑换 (`card_id`是兑换卡的ID，`callback`是回调函数名称)

	native.redeem({
		card_id: 'card_id',
		callback: callback_name
	});

    callback_name({status:1});

    status: 1:成功;

---


- 填写邀请人ID (`inviter_id`是邀请人的ID，`callback`是回调函数名称)

	native.get_inviter({
		inviter_id: 'inviter_id',
		callback: callback_name
	});

    callback_name({status:1});
	这里如果是首页可以多传一个account参数  更新首页积分，也可以通过base.data_refresh方法刷新页面数据

    status: 1:成功;  不是1:失败

---

- web页面加载完成会调用app端`download_start`方法
	native('download_start',{
		callback: callbackname
	});

	callbackname({
		num: -1
	});
---

- web页面获取更新日志（只有安卓）
	native('check_version',{
		callback: callbackname
	});

	callbackname({
		"status": 1,
		"version": "1.2.0",
		"changelogs": "更新说明：<br/>1、新增手机号登入<br/>2、新增手机号绑定解绑<br/>3、优化支付宝绑定及修改 <br/>4、任务界面优化更人性化 <br/>5、修复了少量BUG <br/>6、优化提现界面"
	});
---

- web页面通知客户端更新（只有apple需要传参）
	native('version_refresh', {apple_url: 'https://itunes.apple.com/cn/app/sui-youbi/id1149698186?mt=8'});

	回调内容num是`0`到`100`之间的数字,
	** 如果失败  num传`-1` **
---

- 客户端刷新web页面数据
	base.data_refresh(render_data);

	纯粹的刷新页面会造成页面渲染，js语法解析执行等，开销太大，某些情况下，客户端需要刷新web页面的数据可以通过此方法完成，所有页面（download,download_loading页面除外）都可以通过这个方法刷新页面，render_data是base.render时传的数据格式类型

- （其他遇到再加）
