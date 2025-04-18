---
project: redis
stars: 1757
description: |-
    《Redis Command Reference》全文的中文翻译版。
url: https://github.com/huangzworks/redis
---



<!DOCTYPE html>
<!--[if IE 8]><html class="no-js lt-ie9" lang="en" > <![endif]-->
<!--[if gt IE 8]><!--> <html class="no-js" lang="en" > <!--<![endif]-->
<head>
  <meta charset="utf-8">
  
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <title>关于 &mdash; Redis 命令参考</title>
  

  
  
  
  

  
  <script type="text/javascript" src="_static/js/modernizr.min.js"></script>
  
    
      <script type="text/javascript" id="documentation_options" data-url_root="./" src="_static/documentation_options.js"></script>
        <script type="text/javascript" src="_static/jquery.js"></script>
        <script type="text/javascript" src="_static/underscore.js"></script>
        <script type="text/javascript" src="_static/doctools.js"></script>
        <script type="text/javascript" src="_static/language_data.js"></script>
    
    <script type="text/javascript" src="_static/js/theme.js"></script>

    

  
  <link rel="stylesheet" href="_static/css/theme.css" type="text/css" />
  <link rel="stylesheet" href="_static/pygments.css" type="text/css" />
    <link rel="index" title="Index" href="genindex.html" />
    <link rel="search" title="Search" href="search.html" /> 
</head>

<body class="wy-body-for-nav">

   
  <div class="wy-grid-for-nav">

    
    <nav data-toggle="wy-nav-shift" class="wy-nav-side">
      <div class="wy-side-scroll">
        <div class="wy-side-nav-search">
          

          
            <a href="index.html" class="icon icon-home"> Redis 命令参考
          

          
          </a>

          
            
            
              <div class="version">
                2019
              </div>
            
          

          
<div role="search">
  <form id="rtd-search-form" class="wy-form" action="search.html" method="get">
    <input type="text" name="q" placeholder="Search docs" />
    <input type="hidden" name="check_keywords" value="yes" />
    <input type="hidden" name="area" value="default" />
  </form>
</div>

          
        </div>

        <div class="wy-menu wy-menu-vertical" data-spy="affix" role="navigation" aria-label="main navigation">
          
            
            
              
            
            
              <ul>
<li class="toctree-l1"><a class="reference internal" href="string/index.html">字符串</a></li>
<li class="toctree-l1"><a class="reference internal" href="hash/index.html">哈希表</a></li>
<li class="toctree-l1"><a class="reference internal" href="list/index.html">列表</a></li>
<li class="toctree-l1"><a class="reference internal" href="set/index.html">集合</a></li>
<li class="toctree-l1"><a class="reference internal" href="sorted_set/index.html">有序集合</a></li>
<li class="toctree-l1"><a class="reference internal" href="hyperloglog/index.html">HyperLogLog</a></li>
<li class="toctree-l1"><a class="reference internal" href="geo/index.html">地理位置</a></li>
<li class="toctree-l1"><a class="reference internal" href="bitmap/index.html">位图</a></li>
<li class="toctree-l1"><a class="reference internal" href="database/index.html">数据库</a></li>
<li class="toctree-l1"><a class="reference internal" href="expire/index.html">自动过期</a></li>
<li class="toctree-l1"><a class="reference internal" href="transaction/index.html">事务</a></li>
<li class="toctree-l1"><a class="reference internal" href="script/index.html">Lua 脚本</a></li>
<li class="toctree-l1"><a class="reference internal" href="persistence/index.html">持久化</a></li>
<li class="toctree-l1"><a class="reference internal" href="pubsub/index.html">发布与订阅</a></li>
<li class="toctree-l1"><a class="reference internal" href="replication/index.html">复制</a></li>
<li class="toctree-l1"><a class="reference internal" href="client_and_server/index.html">客户端与服务器</a></li>
<li class="toctree-l1"><a class="reference internal" href="configure/index.html">配置选项</a></li>
<li class="toctree-l1"><a class="reference internal" href="debug/index.html">调试</a></li>
<li class="toctree-l1"><a class="reference internal" href="internal/index.html">内部命令</a></li>
<li class="toctree-l1"><a class="reference internal" href="topic/index.html">功能文档</a></li>
</ul>

            
          
        </div>
      </div>
    </nav>

    <section data-toggle="wy-nav-shift" class="wy-nav-content-wrap">

      
      <nav class="wy-nav-top" aria-label="top navigation">
        
          <i data-toggle="wy-nav-top" class="fa fa-bars"></i>
          <a href="index.html">Redis 命令参考</a>
        
      </nav>


      <div class="wy-nav-content">
        
        <div class="rst-content">
        
          















<div role="navigation" aria-label="breadcrumbs navigation">

  <ul class="wy-breadcrumbs">
    
      <li><a href="index.html">Docs</a> &raquo;</li>
        
      <li>关于</li>
    
    
      <li class="wy-breadcrumbs-aside">
        
            
            <a href="_sources/readme.rst.txt" rel="nofollow"> View page source</a>
          
        
      </li>
    
  </ul>

  
  <hr/>
</div>
          <div role="main" class="document" itemscope="itemscope" itemtype="http://schema.org/Article">
           <div itemprop="articleBody">
            
  <div class="section" id="id1">
<h1>关于<a class="headerlink" href="#id1" title="Permalink to this headline">¶</a></h1>
<p>本文档是 Redis 命令参考手册的中文翻译版，
可以在 <a class="reference external" href="http://www.redisdoc.com">RedisDoc.com</a> 在线阅读本文档。</p>
<div class="section" id="id2">
<h2>版权声明<a class="headerlink" href="#id2" title="Permalink to this headline">¶</a></h2>
<p>本文档由 <a class="reference external" href="http://huangz.me">黄健宏（huangz）</a> 翻译，版权归 Redis 官方所有。</p>
</div>
<div class="section" id="id3">
<h2>赞助商<a class="headerlink" href="#id3" title="Permalink to this headline">¶</a></h2>
<p>本文档由 <a class="reference external" href="http://yunba.io/">云巴（yunba.io）</a> 提供赞助支持。</p>
</div>
</div>


            <div class="section" id="discuss">

    <h2>
        讨论
        <a class="headerlink" href="#discuss" title="永久链接至标题">¶</a>
    </h2>

    <div id="disqus_thread"></div>
    <script type="text/javascript">
        /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
        var disqus_shortname = 'redis-command-cn'; // required: replace example with your forum shortname

        /* * * DON'T EDIT BELOW THIS LINE * * */
        (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
        })();
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    <a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
</div>

<!--
<div id="sponser">
    <h2>赞助商</h2>
    <p>我们正在寻找赞助商，有意对这个网站进行赞助的朋友请联系 huangz1990@gmail.com 。</p>
</div>
-->
           </div>
           
          </div>
          <footer>
  

  <hr/>

  <div role="contentinfo">
    <p>
        &copy; Copyright 2019, Redis

    </p>
  </div>
  Built with <a href="http://sphinx-doc.org/">Sphinx</a> using a <a href="https://github.com/rtfd/sphinx_rtd_theme">theme</a> provided by <a href="https://readthedocs.org">Read the Docs</a>. 

</footer>

        </div>
      </div>

    </section>

  </div>
  


  <script type="text/javascript">
      jQuery(function () {
          SphinxRtdTheme.Navigation.enable(true);
      });
  </script>

  
  
    
   

    <script>
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

    ga('create', 'UA-53959484-7', 'auto');
    ga('send', 'pageview');
  </script>
</body>
</html>
