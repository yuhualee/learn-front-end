### ratchet 开发环境搭建
* 安装 homebrew
		
		brew -v
	如果没打印出正确的版本，则执行以下代码安装

		ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

* 安装 nodejs 
	
		node -v

	如果没打印出正确的版本，则执行以下代码安装
		
		brew install node
		
* 安装 bower 和 gulp* 

		npm install -g bower gulp

* 安装 sass
		
		gem sources --remove https://rubygems.org/
		gem sources -a https://ruby.taobao.org/
		gem sources -l
		sudo gem install sass
		
* 克隆代码
		
		cd ~/code/
		git@github.com:yuhualee/lezyo.git
		cd lezyo
		
* 安装 node 插件
		
		node install
		
* 安装 前端各种包
	
		bower install
    
* 启动开发环境
	
		gulp watch

* 开发完成后编译
	
		gulp build
		
		
		
		
### pjax 的优点
* 下载过的资源不用重新加载，是完全不用加载，而不是304
* 用户体验更好，加载新页面有顶部条了loading
* 参考 http://phphub.org 手机上效果更好

		
