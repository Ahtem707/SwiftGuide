<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bond &amp; ReactiveKit</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p>Библиотека bond для компонентов интерфейса, навешивание событий на компоненты используя лишь Outlet привязку. Также известная как реактивное программирование</p>
<ul>
<li><a href="#%D0%B8%D0%BD%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F">Инициализация</a></li>
<li><a href="#%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5">Использование</a>
<ul>
<li><a href="#%D0%BB%D1%8E%D0%B1%D0%BE%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5-textfield">Любое изменение textField</a></li>
<li><a href="#%D0%BE%D0%B1%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-label-%D0%BF%D1%80%D0%B8-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B8-textfield">Обновление label при изменении textField</a></li>
<li><a href="#%D0%BE%D0%B1%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-label-%D0%BF%D1%80%D0%B8-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B8-textfield-%D1%81-%D0%BF%D1%80%D0%B5%D1%84%D0%B8%D0%BA%D1%81%D0%BE%D0%BC">Обновление label при изменении textField с префиксом</a></li>
<li><a href="#%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D1%81%D0%BE%D0%B1%D1%8B%D1%82%D0%B8%D1%8F-%D0%BD%D0%B0-%D0%BA%D0%BD%D0%BE%D0%BF%D0%BA%D1%83-%D0%BF%D1%80%D0%BE%D1%81%D1%82%D0%BE%D0%B5-%D0%BD%D0%B0%D0%B6%D0%B0%D1%82%D0%B8%D0%B5">Добавление события на кнопку, простое нажатие</a></li>
<li><a href="#%D0%B0%D0%BA%D1%82%D0%B8%D0%B2%D0%B0%D1%86%D0%B8%D1%8F-%D0%BA%D0%BD%D0%BE%D0%BF%D0%BA%D0%B8-%D0%BF%D0%BE-%D1%83%D1%81%D0%BB%D0%BE%D0%B2%D0%B8%D1%8E-%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%B0%D1%86%D0%B8%D0%B8">Активация кнопки по условию валидации</a></li>
<li><a href="#%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BA%D0%B0%D1%81%D1%82%D0%BE%D0%BC%D0%BD%D0%BE%D0%B3%D0%BE-%D1%80%D0%B5%D0%B0%D0%BA%D1%82%D0%B8%D0%B2%D0%BD%D0%BE%D0%B3%D0%BE-%D1%81%D0%B2%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%B0">Создание кастомного реактивного свойства</a></li>
</ul>
</li>
</ul>
<h1 id="инициализация">Инициализация</h1>
<p>В консоли<br>
<code>pod install</code><br>
В файле ‘Podfile’<br>
<code>pod 'Bond'</code><br>
В консоли<br>
<code>pod update</code></p>
<h1 id="использование">Использование</h1>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">import</span> <span class="token builtin">Bond</span>
<span class="token keyword">import</span> <span class="token builtin">ReactiveKit</span>

<span class="token atrule">@IBOutlet</span> <span class="token keyword">weak</span> <span class="token keyword">var</span> button<span class="token punctuation">:</span> <span class="token builtin">UIButton</span><span class="token operator">!</span>
<span class="token atrule">@IBOutlet</span> <span class="token keyword">weak</span> <span class="token keyword">var</span> textField<span class="token punctuation">:</span> <span class="token builtin">UITextField</span><span class="token operator">!</span>
<span class="token atrule">@IBOutlet</span> <span class="token keyword">weak</span> <span class="token keyword">var</span> label<span class="token punctuation">:</span> <span class="token builtin">UITextField</span><span class="token operator">!</span>
</code></pre>
<h3 id="любое-изменение-textfield">Любое изменение textField</h3>
<pre class=" language-swift"><code class="prism  language-swift">textField<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text<span class="token punctuation">.</span>observeNext <span class="token punctuation">{</span> text <span class="token keyword">in</span>
    <span class="token function">print</span><span class="token punctuation">(</span>text<span class="token operator">!</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="обновление-label-при-изменении-textfield">Обновление label при изменении textField</h3>
<pre class=" language-swift"><code class="prism  language-swift">textField<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text<span class="token punctuation">.</span><span class="token function">bind</span><span class="token punctuation">(</span>to<span class="token punctuation">:</span> label<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text<span class="token punctuation">)</span>
<span class="token comment">// Упрощенная форма</span>
textField<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text<span class="token punctuation">.</span><span class="token function">bind</span><span class="token punctuation">(</span>to<span class="token punctuation">:</span> label<span class="token punctuation">)</span>
</code></pre>
<h3 id="обновление-label-при-изменении-textfield-с-префиксом">Обновление label при изменении textField с префиксом</h3>
<pre class=" language-swift"><code class="prism  language-swift">textField<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text
  <span class="token punctuation">.</span><span class="token builtin">map</span> <span class="token punctuation">{</span> <span class="token string">"Hi "</span> <span class="token operator">+</span> $<span class="token number">0</span> <span class="token punctuation">}</span>
  <span class="token punctuation">.</span><span class="token function">bind</span><span class="token punctuation">(</span>to<span class="token punctuation">:</span> label<span class="token punctuation">)</span>
</code></pre>
<h3 id="добавление-события-на-кнопку-простое-нажатие">Добавление события на кнопку простое нажатие</h3>
<pre class=" language-swift"><code class="prism  language-swift">button<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span><span class="token function">controlEvents</span><span class="token punctuation">(</span><span class="token punctuation">.</span>touchUpInside<span class="token punctuation">)</span>
  <span class="token punctuation">.</span>observeNext <span class="token punctuation">{</span> e <span class="token keyword">in</span>
    <span class="token function">print</span><span class="token punctuation">(</span><span class="token string">"Button tapped."</span><span class="token punctuation">)</span>
  <span class="token punctuation">}</span>
<span class="token comment">// Упрощенный аналог</span>
button<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>tap
    <span class="token punctuation">.</span>observeNext <span class="token punctuation">{</span>
      <span class="token function">print</span><span class="token punctuation">(</span><span class="token string">"Button tapped."</span><span class="token punctuation">)</span>
    <span class="token punctuation">}</span>
</code></pre>
<h3 id="активация-кнопки-по-условию-валидации">Активация кнопки по условию валидации</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token function">combineLatest</span><span class="token punctuation">(</span>emailField<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text<span class="token punctuation">,</span> passField<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text<span class="token punctuation">)</span> <span class="token punctuation">{</span> email<span class="token punctuation">,</span> pass <span class="token keyword">in</span>
    <span class="token keyword">return</span> email<span class="token punctuation">.</span>length <span class="token operator">&gt;</span> <span class="token number">0</span> <span class="token operator">&amp;&amp;</span> pass<span class="token punctuation">.</span>length <span class="token operator">&gt;</span> <span class="token number">0</span>
  <span class="token punctuation">}</span>
  <span class="token punctuation">.</span><span class="token function">bind</span><span class="token punctuation">(</span>to<span class="token punctuation">:</span> button<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>isEnabled<span class="token punctuation">)</span>
</code></pre>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token comment">// ??? Использование свойства модели</span>
model<span class="token punctuation">.</span>numberOfFollowers<span class="token punctuation">.</span><span class="token builtin">map</span> <span class="token punctuation">{</span> <span class="token string">"<span class="token interpolation"><span class="token delimiter variable">\(</span>$<span class="token number">0</span><span class="token delimiter variable">)</span></span>"</span> <span class="token punctuation">}</span>
    <span class="token punctuation">.</span><span class="token function">bind</span><span class="token punctuation">(</span>to<span class="token punctuation">:</span> textField2<span class="token punctuation">)</span>
</code></pre>
<h3 id="создание-кастомного-реактивного-свойства">Создание кастомного реактивного свойства</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">extension</span> <span class="token builtin">ReactiveExtensions</span> <span class="token keyword">where</span> <span class="token keyword">Self</span><span class="token punctuation">.</span><span class="token builtin">Base</span> <span class="token punctuation">:</span> <span class="token builtin">UIView</span> <span class="token punctuation">{</span>
    <span class="token keyword">public</span> <span class="token keyword">var</span> isUserEnable<span class="token punctuation">:</span> <span class="token builtin">Bond</span><span class="token operator">&lt;</span><span class="token builtin">Bool</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span>
        <span class="token keyword">get</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> bond <span class="token punctuation">{</span>
                $<span class="token number">0</span><span class="token punctuation">.</span>backgroundColor <span class="token operator">=</span> $<span class="token number">1</span> <span class="token operator">?</span> #<span class="token function">colorLiteral</span><span class="token punctuation">(</span>red<span class="token punctuation">:</span> <span class="token number">0.2549019754</span><span class="token punctuation">,</span> green<span class="token punctuation">:</span> <span class="token number">0.2745098174</span><span class="token punctuation">,</span> blue<span class="token punctuation">:</span> <span class="token number">0.3019607961</span><span class="token punctuation">,</span> alpha<span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token punctuation">:</span> #<span class="token function">colorLiteral</span><span class="token punctuation">(</span>red<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span> green<span class="token punctuation">:</span> <span class="token number">0.5650748014</span><span class="token punctuation">,</span> blue<span class="token punctuation">:</span> <span class="token number">0.3169043064</span><span class="token punctuation">,</span> alpha<span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">)</span>
                $<span class="token number">0</span><span class="token punctuation">.</span>isUserInteractionEnabled <span class="token operator">=</span> <span class="token operator">!</span>$<span class="token number">1</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="пример-валидация-textfield">Пример валидация textField</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token comment">// Ввод исключительно чисел и ограничение по количеству символов</span>
textField<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text
    <span class="token punctuation">.</span><span class="token builtin">map</span> <span class="token punctuation">{</span>
        <span class="token keyword">if</span> $<span class="token number">0</span><span class="token operator">?</span><span class="token punctuation">.</span><span class="token builtin">last</span><span class="token operator">?</span><span class="token punctuation">.</span>isNumber <span class="token operator">?</span><span class="token operator">?</span> <span class="token boolean">false</span> <span class="token operator">&amp;&amp;</span> $<span class="token number">0</span><span class="token operator">!</span><span class="token punctuation">.</span><span class="token builtin">count</span> <span class="token operator">&lt;=</span> <span class="token number">5</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> $<span class="token number">0</span><span class="token operator">!</span>
        <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token function">String</span><span class="token punctuation">(</span>$<span class="token number">0</span><span class="token operator">!</span><span class="token punctuation">.</span><span class="token keyword">prefix</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token punctuation">(</span>$<span class="token number">0</span><span class="token operator">!</span><span class="token punctuation">.</span><span class="token builtin">count</span> <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token operator">?</span> <span class="token number">1</span> <span class="token punctuation">:</span> $<span class="token number">0</span><span class="token operator">!</span><span class="token punctuation">.</span><span class="token builtin">count</span><span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
    <span class="token punctuation">.</span><span class="token function">bind</span><span class="token punctuation">(</span>to<span class="token punctuation">:</span> textField<span class="token punctuation">.</span>reactive<span class="token punctuation">.</span>text<span class="token punctuation">)</span>
</code></pre>
</div>
</body>

</html>
