<template>
    <div class="shareArea cflex">
		<p class="shareTitle">分享组件一：横向排列</p>
		<div class="bottom rflex">
			<span class="toTitle">分享到：</span>
			<ul class="shareUl rflex wflex">
				<li>
					<div class="item" @mouseover="showqrcode()" @mouseout="hideqrcode()">
						<icon-svg icon-class="iconwechat" />
					</div>
					<div class="qrcodeArea" v-show="qrcode.show">
						<p class="saoTitle">扫一扫</p>
						<div class="qrcode" ref="qrCodeUrl" ></div>
					</div>
				</li>
				<li>
					<div class="item" @click="shareToWeibo()">
						<icon-svg icon-class="iconweibo" />
					</div>
				</li>
				<li>
					<div class="item" @click="shareToQQ()">
						<icon-svg icon-class="iconqq" />
					</div>
				</li>
				<li>
					<div class="item" @click="shareToQQzone()">
						<icon-svg icon-class="iconqq_zone" />
					</div>
				</li>
			
				<li>
					<div class="item" @click="shareToDouban()">
						<icon-svg icon-class="icondouban" />
					</div>
				</li>
			</ul>
		</div>
    </div>
</template>

<script>
	import QRCode from 'qrcodejs2'
	import { shareUrl } from "@/utils/env";

	export default {
	  name:'YanShare',
	  data(){
			return {
				qrcode:{
					show:false
				},
				qrcodeObj:{
					text:shareUrl, // 要分享的网页路径
					width:80,
					height:80,
					colorDark: '#000000',
					colorLight: '#ffffff',
					correctLevel: QRCode.CorrectLevel.H
				}
				
			}
		},
		mounted(){
			this.creatQrCode();
		},
		methods: {
			showqrcode(){
				this.qrcode.show  = true;
			},
			hideqrcode(){
				this.qrcode.show  = false;
			},
			creatQrCode() {
				 const qrcode = new QRCode(this.$refs.qrCodeUrl, this.qrcodeObj)
			},
			shareToQQ(){
                this.$emit('shareToQQ');
			},
			shareToQQzone(){
                this.$emit('shareToQQzone');
			},
			shareToWeibo(){
                this.$emit('shareToWeibo');
            },
			shareToDouban(){
                this.$emit('shareToDouban');
			}

		}
	}
</script>

<style lang="less" scoped>
	.shareArea{
		width: 340px;
		align-items: center;
		background: #fff;
		border-radius: 4px;
         .shareTitle{
            border-bottom: 1px solid #e8e8e8;
            padding: 10px;
            box-sizing: border-box;
            width: 100%;
            font-size:14px;
        }
		.bottom{
			align-items: center;
			padding: 20px;
			width: 100%;
			height: 100%;
			box-sizing: border-box;
			.toTitle{
				font-size: 13px;
			}
			 .shareUl{
				justify-content: space-between;
				li{
					display: flex;
					flex-direction: column;
					align-items: center;
					position: relative;
					cursor: pointer;
					.title{
						margin-bottom: 10px;
						font-size: 13px;
						color:#a9d86e;
					}
					.item{
						background: #EFF2F7;
						width: 40px;
						height: 40px;
						border-radius: 50%;
						display: flex;
						justify-content: center;
						align-items: center;
						.svg-icon{
							font-size: 24px;
						}
						.active{
							color:#FF6C60;
						}
					}
					.qrcodeArea{
						position: absolute;
						top: 50px;
						left: -30px;
						text-align: center;
						border: 1px solid #a9d86e;
						border-radius: 4px;
						padding: 10px;
						.saoTitle{
								font-size: 14px;
							color:#a9d86e;
							margin-bottom: 5px;
						}
					}
				}
			}
		}
     
	}
	
</style>
