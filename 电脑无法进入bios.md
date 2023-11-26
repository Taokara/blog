# 电脑无法进入bios
<style>
.blogpost-body h2{
    font-size: 28px;
    font-weight: bold;
    height: 37px;
    border-bottom: 3px solid #000000;
	padding-top:0.3cm;
}
h3{
    background: linear-gradient(to right, #2a5caa 0%,#ffffff 100%);
    color: #FFFFFF;
    font-size: 18px;
    font-weight: bold;
    height: 30px;
    padding: 8px 0 5px 10px;
    text-shadow: 2px 2px 3px #222222;
}
h4{
    background: linear-gradient(to right, #99cc99 0%,#ffffff 100%);
	color: #003300;
    font-weight: bold;
    height: 25px;
    padding: 1px 0 5px 5px;
}
h5{
    background: linear-gradient(to right, #BEBEBE 0%,#ffffff 100%);
	color: #003300;
    /* font-weight: bold; */
    height: 17px;
    padding: 1px 0 5px 5px;
}
img {
display: block;
margin: auto;
}
</style>
1. 说明
	我的双屏电脑重启不会显示品牌图标，按delete键也不能进入bios
1. 解决
	好像是因为nvida 20系显卡驱动的问题，只能用HDMI线连接的显示屏才能正常进入bios，于是我拔掉DP线连接的显示器，即可正常进入bios。