<template lang="jade">
	div.social-share
		a.social-share-icon.icon-weibo(target="_blank", :href="'http://v.t.sina.com.cn/share/share.php?url='+ url +'&title='+ title +'&pic='+ image")
			i.fa.fa-weibo
		a.social-share-icon.icon-wechat(href="#")
			i.fa.fa-weixin
			div.wechat-qrcode(:class="{bottom: QCodePosition}")
				h4 微信扫一扫：分享
				div.qrcode
					qrcode(:value="url", type="image", :size="112")
				div.help
					<p>微信里点“发现”，扫一下</p><p>二维码便可将本文分享至朋友圈。</p>
		a.social-share-icon.icon-qq(target="_blank", :href="'http://connect.qq.com/widget/shareqq/index.html?url=' + url + '&title=' + title + '&source=' + source + '&desc=' + description + '&pics=' + image")
			i.fa.fa-qq
		a.social-share-icon.icon-qzone(target="_blank", :href="'http://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey?url=' + url + '&title=' + title + '&desc=' + description + '&summary=' + summary + '&site=' + source")
			i.fa.fa-star
</template>
<script>
    import Vue from 'vue'
    import Qrcode from 'v-qrcode'
    export default{
        name: 'share',
        props:{
        	url: {
        		type: String,
        		default: location.href
        	},
        	title: {
        		type: String,
        		default: document.getElementsByName('title')[0].content || document.title || ''
        	},
        	image: {
        		type: String,
        		default: (document.images[0] || 0).src || 'http://www.sharewuji.com.img.800cdn.com/assets/images/icon.png'
        	},
        	description:{
        		type: String,
        		default: document.getElementsByName('description')[0].content || ''
        	},
        	summary: {
        		type: String,
        		default: ''
        	},
        	source: {
        		type: String,
        		default: '吾记'
        	},
        	QCodePosition: {
        		type: Boolean,
        		default: false
        	}
        },
        components: {
        	Qrcode
        }
    }
</script>
<style lang="sass">
	@import "../public/scss/_variables.scss";
	.social-share {
	  a {
	    position:relative;
	    text-decoration:none;
	    margin: 4px;
	    display:inline-block;
	    outline: none;
	  }

	  .social-share-icon {
	    position:relative;
	    display:inline-block;
	    width: 32px;
	    height: 32px;
	    font-size: $size-h3;
	    border-radius: 50%;
	    line-height: 32px;
	    border:1px solid $gray;
	    color: $gray;
	    text-align: center;
	    vertical-align: middle;
	    transition: background 0.6s ease-out 0s;

	    &:hover{
	      background: $gray;
	      color: $white;
	    }
	  }

	  .icon-weibo{
	    color:#ff763b;
	    border-color:#ff763b;
	    &:hover{
	      background:#ff763b;
	    }
	  }
	  .icon-qq{
	    color:#56b6e7;
	    border-color:#56b6e7;
	    &:hover{
	      background:#56b6e7;
	    }
	  }
	  .icon-qzone{
	    color:#FDBE3D;
	    border-color:#FDBE3D;
	    &:hover{
	      background:#FDBE3D;
	    }
	  }
	  .icon-wechat{
	    position:relative;
	    color:#7bc549;
	    border-color:#7bc549;
	    &:hover{
	      background:#7bc549;
	    }
	  }
	  .icon-wechat .wechat-qrcode{
	  	display: none;
	  	border: 1px solid #eee;
	  	position: absolute;
	  	z-index: 9;
	  	top: -205px;
	  	left: -84px;
	  	width: 200px;
	  	height: 192px;
	  	color: $gray;
	  	font-size: $size-h5;
	  	text-align: center;
	  	background-color: $white;
	  	box-shadow: 0 2px 10px #aaa;
	  	transition: all 200ms;
	  }
	  .icon-wechat .wechat-qrcode.bottom {
	    top: 49px;
	    left: -71px;
	    &:after {
	      display:none;
	    }
	  }
	  .icon-wechat .wechat-qrcode h4{
	  	font-weight: normal;
	  	height: 26px;
	  	line-height: 26px;
	  	font-size: $size-h5;
	  	background-color: #f3f3f3; 
	  	margin: 0;
	  	padding: 0;
	  	color: #777;
	  }
	  .icon-wechat .wechat-qrcode .qrcode{
	  	margin: 10px auto;
	  }
	  .icon-wechat .wechat-qrcode .qrcode table{
	  	margin: 0!important;
	  }
	  .icon-wechat .wechat-qrcode .help p{
	  	font-weight: normal;
	  	line-height: 16px;
	  	padding: 0;
	  	margin: 0;
	  }
	  .icon-wechat .wechat-qrcode:after{
	  	content: '';
	  	position: absolute;
	  	left: 50%;
	  	margin-left: -6px;
	  	bottom: -13px;
	  	width: 0;
	  	height: 0;
	  	border-width: 8px 6px 6px 6px;
	  	border-style: solid;
	  	border-color: $white transparent transparent transparent;
	  }
	  .icon-wechat:hover .wechat-qrcode{
	  	display: block;
	  }
	}
</style>