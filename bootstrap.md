# 导航

## nav 配合<div>使用

    .nav 生成导航栏
    .nav-pills 胶囊状导航 <ul>
    .nav-tabs 标签式导航 <ul>
    .nav-link 链接样式 <a>
    .nav-divider 导航分割线 <li>
    .nav-stacked 垂直 导航 <ul>
    .nav-justified 自适应导航 <ul>
    下拉菜单的实例
    <ul class="nav nav-tabs">
        <li class="active"><a href="#">Home</a></li>
        <li><a href="#">SVN</a></li>
        <li><a href="#">iOS</a></li>
        <li><a href="#">VB.Net</a></li>
        <li class="dropdown">
            <a class="dropdown-toggle" data-toggle="dropdown" href="#">
            Java <span class="caret"></span>
            </a>
            <ul class="dropdown-menu">
            <li><a href="#">Swing</a></li>
            <li><a href="#">jMeter</a></li>
            <li><a href="#">EJB</a></li>
            <li class="divider"></li>
            <li><a href="#">分离的链接</a></li>
            </ul>
        </li>
        <li><a href="#">PHP</a></li>
    </ul>
    对<li>使用dropdowm来实现

## breadcrumb

    面包式导航
    首页/简介/个人信息
    一般使用<ol>

## navbar 配合<nav>使用（折叠式导航）

    .navbar 生成导航栏
    .navbar-expend-xx xx为sm、lg等等 表示响应式导航
    .bg-xx 背景颜色
    .flex-top 固定顶端
    .navbar-nav 用于<ul>
    .nav-item 用于<li>
    .nav-link 用于<a>
    .navbar-text 用于文本
    一个折叠导航的实例
        <nav class="navbar navbar-expand-md bg-dark navbar-dark">
            <!-- 品牌 -->
            <a href="#" class="navbar-brand">品牌LOGO</a>

            <!-- 定义折叠按钮 -->
            <button type="button" class="navbar-toggler" data-toggle="collapse" data-target="#nav-menu">
                <span class="navbar-toggler-icon"></span>
            </button>
            <!-- 把菜单包含在容器内 -->
            <div class="collapse navbar-collapse" id="nav-menu">
                <ul class="navbar-nav">
                <li class="nav-item active"><a href="#" class="nav-link">菜单一</a></li>
                <li class="nav-item"><a href="#" class="nav-link">菜单二</a></li>
                <li class="nav-item"><a href="#" class="nav-link disabled">菜单三</a></li>
                </ul>
            </div>
        </nav>
    .navbar-brand 导航LOGO
    data-toggle 触发的事件
    data-target 触发的内容
    collapse 折叠
    flex-column 垂直导航 用于<ul>
