<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Delegate and Callback</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><ul>
<li><a href="#%D0%B4%D0%B5%D0%BB%D0%B5%D0%B3%D0%B0%D1%82%D1%8B">Делегаты</a>
<ul>
<li><a href="#%D0%B4%D0%B5%D0%BB%D0%B5%D0%B3%D0%B0%D1%82-%D1%81-%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D0%BE%D0%BC">Делегат с протоколом</a></li>
<li><a href="#%D0%B4%D0%B5%D0%BB%D0%B5%D0%B3%D0%B0%D1%82-%D0%B1%D0%B5%D0%B7-%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D0%B0">Делегат без протокола</a></li>
</ul>
</li>
<li><a href="#callback">Callback</a></li>
</ul>
<h1 id="делегаты">Делегаты</h1>
<h3 id="делегат-с-протоколом">Делегат с протоколом</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">class</span>  <span class="token class-name">SenderClass1</span> <span class="token punctuation">{</span>
	<span class="token keyword">var</span> delegate<span class="token punctuation">:</span> <span class="token builtin">ReceiveClassDelegate</span><span class="token operator">?</span>
	<span class="token comment">// using</span>
	<span class="token keyword">func</span>  <span class="token function">viewDidLoad</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">self</span><span class="token punctuation">.</span>delegate<span class="token operator">?</span><span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">"hi"</span><span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">class</span>  <span class="token class-name">ReceiveClass1</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span>  senderClass <span class="token operator">=</span> <span class="token function">SenderClass1</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
	<span class="token keyword">func</span> <span class="token function">viewDidLoad</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">self</span><span class="token punctuation">.</span>senderClass<span class="token punctuation">.</span>delegate <span class="token operator">=</span> <span class="token keyword">self</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
protocol <span class="token builtin">ReceiveClassDelegate1</span> <span class="token punctuation">{</span>
	<span class="token keyword">func</span> <span class="token function">send</span><span class="token punctuation">(</span><span class="token number">_</span> a<span class="token punctuation">:</span> <span class="token builtin">String</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
<span class="token keyword">extension</span>  <span class="token builtin">ReceiveClass1</span><span class="token punctuation">:</span> <span class="token builtin">ReceiveClassDelegate1</span> <span class="token punctuation">{</span>
	<span class="token keyword">func</span> <span class="token function">send</span><span class="token punctuation">(</span><span class="token number">_</span> a<span class="token punctuation">:</span> <span class="token builtin">String</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token function">print</span><span class="token punctuation">(</span>a<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="делегат-без-протокола">Делегат без протокола</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">class</span> <span class="token class-name">SenderClass2</span> <span class="token punctuation">{</span>
    <span class="token keyword">var</span> delegate<span class="token punctuation">:</span> <span class="token builtin">ReceiveClass2</span><span class="token operator">?</span>
    <span class="token comment">// using</span>
    <span class="token keyword">func</span> <span class="token function">viewDidLoad</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">self</span><span class="token punctuation">.</span>delegate<span class="token operator">?</span><span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">"hi"</span><span class="token punctuation">)</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">class</span> <span class="token class-name">ReceiveClass2</span> <span class="token punctuation">{</span>
    <span class="token keyword">let</span> senderClass <span class="token operator">=</span> <span class="token function">SenderClass2</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
    <span class="token keyword">func</span> <span class="token function">viewDidLoad</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">self</span><span class="token punctuation">.</span>senderClass<span class="token punctuation">.</span>delegate <span class="token operator">=</span> <span class="token keyword">self</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">extension</span> <span class="token builtin">ReceiveClass2</span> <span class="token punctuation">{</span>
    <span class="token keyword">func</span> <span class="token function">send</span><span class="token punctuation">(</span><span class="token number">_</span> a<span class="token punctuation">:</span> <span class="token builtin">String</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token function">print</span><span class="token punctuation">(</span>a<span class="token punctuation">)</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h1 id="callback">Callback</h1>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">class</span> <span class="token class-name">SenderClass3</span> <span class="token punctuation">{</span>
	<span class="token keyword">var</span> sender<span class="token punctuation">:</span> <span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token builtin">String</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">Void</span><span class="token punctuation">)</span><span class="token operator">?</span>
	<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
	sender<span class="token operator">?</span><span class="token punctuation">(</span><span class="token string">"hi"</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
<span class="token keyword">class</span> <span class="token class-name">ReceiveClass3</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span> model <span class="token operator">=</span> <span class="token function">SenderClass3</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
	model<span class="token punctuation">.</span>sender <span class="token operator">=</span> <span class="token punctuation">{</span> <span class="token punctuation">[</span><span class="token keyword">weak</span> <span class="token keyword">self</span><span class="token punctuation">]</span> <span class="token punctuation">(</span>str<span class="token punctuation">)</span> <span class="token keyword">in</span>
		<span class="token keyword">self</span><span class="token operator">?</span><span class="token punctuation">.</span><span class="token function">printer</span><span class="token punctuation">(</span>str<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
	<span class="token keyword">func</span> <span class="token function">printer</span><span class="token punctuation">(</span><span class="token number">_</span> str<span class="token punctuation">:</span> <span class="token builtin">String</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token function">print</span><span class="token punctuation">(</span>str<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
</div>
</body>

</html>
