<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NavigationController</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><ul>
<li><a href="#%D0%B8%D0%BD%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F">Инициализация</a></li>
<li><a href="#%D0%BF%D0%B5%D1%80%D0%B5%D1%85%D0%BE%D0%B4%D1%8B">Переходы</a></li>
</ul>
<h1 id="инициализация">Инициализация</h1>
<p>SceneDelegate</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">var</span> window<span class="token punctuation">:</span> <span class="token builtin">UIWindow</span><span class="token operator">?</span>
<span class="token comment">// Где MapViewController - стартовый ViewController</span>
<span class="token keyword">var</span> navControl <span class="token operator">=</span> <span class="token function">UINavigationController</span><span class="token punctuation">(</span>rootViewController<span class="token punctuation">:</span> <span class="token function">MapViewController</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">func</span> <span class="token function">scene</span><span class="token punctuation">(</span><span class="token number">_</span> scene<span class="token punctuation">:</span> <span class="token builtin">UIScene</span><span class="token punctuation">,</span> willConnectTo session<span class="token punctuation">:</span> <span class="token builtin">UISceneSession</span><span class="token punctuation">,</span> options connectionOptions<span class="token punctuation">:</span> <span class="token builtin">UIScene</span><span class="token punctuation">.</span><span class="token builtin">ConnectionOptions</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">guard</span> <span class="token keyword">let</span> windowScene <span class="token operator">=</span> <span class="token punctuation">(</span>scene <span class="token keyword">as</span><span class="token operator">?</span> <span class="token builtin">UIWindowScene</span><span class="token punctuation">)</span> <span class="token keyword">else</span> <span class="token punctuation">{</span> <span class="token keyword">return</span> <span class="token punctuation">}</span>
    window <span class="token operator">=</span> <span class="token function">UIWindow</span><span class="token punctuation">(</span>frame<span class="token punctuation">:</span> windowScene<span class="token punctuation">.</span>coordinateSpace<span class="token punctuation">.</span>bounds<span class="token punctuation">)</span>
    window<span class="token operator">?</span><span class="token punctuation">.</span>windowScene <span class="token operator">=</span> windowScene
    window<span class="token operator">?</span><span class="token punctuation">.</span>rootViewController <span class="token operator">=</span> <span class="token keyword">self</span><span class="token punctuation">.</span>navControl
    window<span class="token operator">?</span><span class="token punctuation">.</span><span class="token function">makeKeyAndVisible</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<h1 id="переходы">Переходы</h1>
<p>Переход с одного ViewControllera на другой</p>
<pre class=" language-swift"><code class="prism  language-swift">navigationController<span class="token operator">?</span><span class="token punctuation">.</span><span class="token function">pushViewController</span><span class="token punctuation">(</span><span class="token function">ViewController</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">)</span>
</code></pre>
</div>
</body>

</html>
