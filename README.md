#基于 jQuery 的前端表单验证插件

使用时需进行配置

	validType       验证类型 对象集合 每一个属性都是一种验证类别 每一个属性对应一个对象该对象中的属性名 对应着执行验证的方法 值为提示信息

    validMethods    验证方法 对象集合 每一个方法都是使用 apply 方式被调用，方法中的 this 是进行验证的 jQuery 对象，目前插件中已经设置了常见的验证方法

对每个 input 标签、select 标签、textarea 标签添加属性 data-validator 并设置验证类型

JavaScript 代码：

	$(function(){
	    $.validator.validType.username = {// 用户名 验证配置
	        type: ['required', '请填写用户名'],
	        trim: true, // 验证时对值进行 trim
	        focus: '请输入6~12位数字、字母、下划线组合，并以字母开头', // 获得焦点时的操作
	        valid:[
	            ['regexp', /^[a-z]/i],
	            ['regexp', /^[a-z0-9_]$/i],
	            ['length', 6, 20],
	            ['ajax', 'url', '']
	        ],
	        text:['只能字母开头', '只能输入数字、字母、下划线组合', '只能输入6~12位字符', '该用户名已被注册，请尝试其他用户名'],
	        right:'',
	        callback:function(rs){alert(rs?'通过验证':'未通过验证')} // 验证后的回调函数
	    };
	    var $userNameForm = $.validator({
	        selector: '#userNameForm',
	        normal:function(txt){
	            this.next().empty();
	        },
	        focus:function(txt){
	            this.next().html( txt );
	        },
	        wrong:function(txt){
	            alert(txt);
	        },
	        right:function(txt){
	            alert('通过验证');
	        }
	    });
	});

HTML 代码：

	<form id="userNameForm" action="">
		<input type="text" name="username" id="username" data-validator="username" /><span></span>
	</form>