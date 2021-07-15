<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>YooKassa</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><p>Новая надпись</p>
<ul>
<li><a href="#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0">Установка</a></li>
<li><a href="#%D0%B8%D0%BD%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F">Инициализация</a></li>
<li><a href="#%D0%B8%D0%BD%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F">Серверная часть</a></li>
</ul>
<h3 id="полезные-ссылки">Полезные ссылки</h3>
<ul>
<li><a href="https://yookassa.ru/developers/payments/sdk-tokens?lang=php">Документация YooKassa</a></li>
<li><a href="https://yookassa.ru/developers/api?lang=php#create_payment">Справочник YooKassa, примеры кода сервера</a></li>
</ul>
<h1 id="установка">Установка</h1>
<p>В консоли<br>
<code>pod install</code><br>
В файле ‘Podfile’</p>
<pre><code>pod 'YooKassaPayments',
    :git =&gt; 'https://github.com/yoomoney/yookassa-payments-swift.git',
    :tag =&gt; '6.0.0'
</code></pre>
<p>В консоли<br>
<code>pod update</code></p>
<h1 id="инициализация">Инициализация</h1>
<p>Импорт библиотеки YooKassa</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">import</span> <span class="token builtin">YooKassaPayments</span>
</code></pre>
<p>Объявление свойств</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">final</span>  <span class="token keyword">let</span>  clientApplicationKey <span class="token operator">=</span> <span class="token string">"test_ODExMzkxT6xTXvpxnOTT4nVxxSK5vJTUMjL47pzIFYY"</span>  <span class="token comment">// Ключ приложения</span>
<span class="token keyword">final</span>  <span class="token keyword">let</span>  moneyAuthClientId <span class="token operator">=</span> <span class="token string">"idUser1"</span>  <span class="token comment">// Уникальный идентификатор пользователя, привязан к аккаунту</span>

<span class="token comment">// Отображаемые данные, но не действительные</span>
<span class="token keyword">let</span> shopName <span class="token operator">=</span> <span class="token string">"AliBaba"</span>  <span class="token comment">// Название магазина</span>
<span class="token keyword">let</span> amount <span class="token operator">=</span> <span class="token function">Amount</span><span class="token punctuation">(</span>value<span class="token punctuation">:</span> <span class="token number">999.99</span><span class="token punctuation">,</span> currency<span class="token punctuation">:</span> <span class="token punctuation">.</span>rub<span class="token punctuation">)</span> <span class="token comment">// Сумма и валюта покупки</span>
<span class="token keyword">let</span>  purchaseDescription <span class="token operator">=</span> <span class="token string">"Пакет гороха"</span>  <span class="token comment">// Описание покупки</span>
<span class="token keyword">var</span>  inputData<span class="token punctuation">:</span> <span class="token builtin">TokenizationFlow</span><span class="token operator">?</span>
</code></pre>
<p>Инициализация во viewDidLoad()</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">override</span>  <span class="token keyword">func</span>  <span class="token function">viewDidLoad</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">super</span><span class="token punctuation">.</span><span class="token function">viewDidLoad</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
	<span class="token keyword">let</span> tokenizationModuleInputData <span class="token operator">=</span> <span class="token function">TokenizationModuleInputData</span><span class="token punctuation">(</span>
		clientApplicationKey<span class="token punctuation">:</span> clientApplicationKey<span class="token punctuation">,</span>
		shopName<span class="token punctuation">:</span> shopName<span class="token punctuation">,</span>
		purchaseDescription<span class="token punctuation">:</span> purchaseDescription<span class="token punctuation">,</span>
		amount<span class="token punctuation">:</span> amount<span class="token punctuation">,</span>
		gatewayId<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		tokenizationSettings<span class="token punctuation">:</span> <span class="token function">TokenizationSettings</span><span class="token punctuation">(</span>paymentMethodTypes<span class="token punctuation">:</span> <span class="token punctuation">.</span>all<span class="token punctuation">,</span> showYooKassaLogo<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
		testModeSettings<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		cardScanning<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		applePayMerchantIdentifier<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		returnUrl<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		isLoggingEnabled<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span>
		userPhoneNumber<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		customizationSettings<span class="token punctuation">:</span> <span class="token function">CustomizationSettings</span><span class="token punctuation">(</span>mainScheme<span class="token punctuation">:</span> <span class="token punctuation">.</span>blue<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token comment">// Цвет некоторых элементов модального окна</span>
		savePaymentMethod<span class="token punctuation">:</span> <span class="token punctuation">.</span>off<span class="token punctuation">,</span> <span class="token comment">// Возможность создания автоплатежа</span>
		moneyAuthClientId<span class="token punctuation">:</span> moneyAuthClientId<span class="token punctuation">,</span>
		applicationScheme<span class="token punctuation">:</span> <span class="token constant">nil</span>
	<span class="token punctuation">)</span>
	<span class="token keyword">self</span><span class="token punctuation">.</span>inputData <span class="token operator">=</span> <span class="token punctuation">.</span><span class="token function">tokenization</span><span class="token punctuation">(</span>tokenizationModuleInputData<span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Активация начала платежа</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token atrule">@IBAction</span> <span class="token keyword">func</span> <span class="token function">buy</span><span class="token punctuation">(</span><span class="token number">_</span> sender<span class="token punctuation">:</span> <span class="token builtin">Any</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">guard</span> <span class="token keyword">let</span> inputData <span class="token operator">=</span> inputData <span class="token keyword">else</span> <span class="token punctuation">{</span><span class="token keyword">return</span><span class="token punctuation">}</span>
	<span class="token keyword">let</span> viewController <span class="token operator">=</span> <span class="token builtin">TokenizationAssembly</span><span class="token punctuation">.</span><span class="token function">makeModule</span><span class="token punctuation">(</span>inputData<span class="token punctuation">:</span> inputData<span class="token punctuation">,</span> moduleOutput<span class="token punctuation">:</span> <span class="token keyword">self</span><span class="token punctuation">)</span>
	<span class="token function">present</span><span class="token punctuation">(</span>viewController<span class="token punctuation">,</span> animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span> completion<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">)</span> <span class="token comment">// Отображается модальное окно выбора способа оплаты</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Расширения обработки событий</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">extension</span>  <span class="token builtin">InitialViewController</span><span class="token punctuation">:</span> <span class="token builtin">TokenizationModuleOutput</span> <span class="token punctuation">{</span>
	<span class="token comment">// Будет вызван, когда пользователь не завершил оплату и не завершил работу.</span>
	<span class="token keyword">func</span>  <span class="token function">didFinish</span><span class="token punctuation">(</span>on module<span class="token punctuation">:</span> <span class="token builtin">TokenizationModuleInput</span><span class="token punctuation">,</span> with error<span class="token punctuation">:</span> <span class="token builtin">YooKassaPaymentsError</span><span class="token operator">?</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token builtin">DispatchQueue</span><span class="token punctuation">.</span>main<span class="token punctuation">.</span>async <span class="token punctuation">{</span> <span class="token punctuation">[</span><span class="token keyword">weak</span> <span class="token keyword">self</span><span class="token punctuation">]</span> <span class="token keyword">in</span>
			<span class="token keyword">guard</span>  <span class="token keyword">let</span>  <span class="token keyword">self</span> <span class="token operator">=</span> <span class="token keyword">self</span>  <span class="token keyword">else</span> <span class="token punctuation">{</span> <span class="token keyword">return</span> <span class="token punctuation">}</span>
			<span class="token keyword">self</span><span class="token punctuation">.</span><span class="token function">dismiss</span><span class="token punctuation">(</span>animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">)</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
	<span class="token comment">// Будет вызван, когда 3-D безопасный процесс успешно пройдет.</span>
	<span class="token keyword">func</span>  <span class="token function">didSuccessfullyPassedCardSec</span><span class="token punctuation">(</span>on module<span class="token punctuation">:</span> <span class="token builtin">TokenizationModuleInput</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token punctuation">}</span>
	<span class="token comment">// Будет вызван, когда процесс подтверждения успешно пройдет.</span>
	<span class="token keyword">func</span>  <span class="token function">didSuccessfullyConfirmation</span><span class="token punctuation">(</span>paymentMethodType<span class="token punctuation">:</span> <span class="token builtin">PaymentMethodType</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token builtin">DispatchQueue</span><span class="token punctuation">.</span>main<span class="token punctuation">.</span>async <span class="token punctuation">{</span> <span class="token punctuation">[</span><span class="token keyword">weak</span> <span class="token keyword">self</span><span class="token punctuation">]</span> <span class="token keyword">in</span>
			<span class="token keyword">guard</span>  <span class="token keyword">let</span>  <span class="token keyword">self</span> <span class="token operator">=</span> <span class="token keyword">self</span>  <span class="token keyword">else</span> <span class="token punctuation">{</span> <span class="token keyword">return</span> <span class="token punctuation">}</span>
			<span class="token comment">// Экран успеха после прохождения подтверждения (3DS или Sberpay)</span>
			<span class="token keyword">let</span> paySuccessVC <span class="token operator">=</span> <span class="token function">PaySuccessViewController</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
			paySuccessVC<span class="token punctuation">.</span>parentDelegate <span class="token operator">=</span> <span class="token keyword">self</span>
			<span class="token keyword">self</span><span class="token punctuation">.</span><span class="token function">dismiss</span><span class="token punctuation">(</span>animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">)</span>
			<span class="token comment">// Показать экран успеха</span>
			<span class="token keyword">self</span><span class="token punctuation">.</span>navigationController<span class="token operator">?</span><span class="token punctuation">.</span><span class="token function">pushViewController</span><span class="token punctuation">(</span>paySuccessVC<span class="token punctuation">,</span> animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">)</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
	<span class="token comment">// Будет вызван, когда процесс токенизации успешно пройдет.</span>
	<span class="token keyword">func</span>  <span class="token function">tokenizationModule</span><span class="token punctuation">(</span><span class="token number">_</span> module<span class="token punctuation">:</span> <span class="token builtin">TokenizationModuleInput</span><span class="token punctuation">,</span> didTokenize token<span class="token punctuation">:</span> <span class="token builtin">Tokens</span><span class="token punctuation">,</span> paymentMethodType<span class="token punctuation">:</span> <span class="token builtin">PaymentMethodType</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token builtin">DispatchQueue</span><span class="token punctuation">.</span>main<span class="token punctuation">.</span>async <span class="token punctuation">{</span> <span class="token punctuation">[</span><span class="token keyword">weak</span> <span class="token keyword">self</span><span class="token punctuation">]</span> <span class="token keyword">in</span>
			<span class="token keyword">guard</span>  <span class="token keyword">let</span>  <span class="token keyword">self</span> <span class="token operator">=</span> <span class="token keyword">self</span>  <span class="token keyword">else</span> <span class="token punctuation">{</span> <span class="token keyword">return</span> <span class="token punctuation">}</span>
			<span class="token keyword">self</span><span class="token punctuation">.</span><span class="token function">dismiss</span><span class="token punctuation">(</span>animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">)</span>
		<span class="token punctuation">}</span>
		<span class="token comment">// Отправьте токен в вашу систему</span>
		<span class="token keyword">let</span> model <span class="token operator">=</span> <span class="token function">Payment</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
		model<span class="token punctuation">.</span><span class="token function">sendPayment</span><span class="token punctuation">(</span>token<span class="token punctuation">:</span> token<span class="token punctuation">.</span>paymentToken<span class="token punctuation">,</span> idOrder<span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">(</span>response<span class="token punctuation">,</span>error<span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">Void</span>  <span class="token keyword">in</span>
			<span class="token keyword">if</span> <span class="token keyword">let</span> error <span class="token operator">=</span> error <span class="token punctuation">{</span>
				<span class="token function">print</span><span class="token punctuation">(</span>error<span class="token punctuation">)</span>
				<span class="token keyword">return</span>
			<span class="token punctuation">}</span>
			<span class="token keyword">guard</span> <span class="token keyword">let</span> status <span class="token operator">=</span> response<span class="token operator">?</span><span class="token punctuation">[</span><span class="token string">"status"</span><span class="token punctuation">]</span> <span class="token keyword">as</span><span class="token operator">?</span> <span class="token builtin">String</span> <span class="token keyword">else</span> <span class="token punctuation">{</span><span class="token keyword">return</span><span class="token punctuation">}</span>
			<span class="token keyword">if</span> <span class="token punctuation">(</span>status <span class="token operator">==</span> <span class="token string">"succeeded"</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
				<span class="token keyword">let</span> animationOption <span class="token operator">=</span> <span class="token builtin">UIView</span><span class="token punctuation">.</span><span class="token builtin">AnimationOptions</span><span class="token punctuation">.</span>showHideTransitionViews
				<span class="token keyword">let</span> vc <span class="token operator">=</span> <span class="token function">PaySuccessViewController</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
				vc<span class="token punctuation">.</span>parentDelegate <span class="token operator">=</span> <span class="token keyword">self</span>
				<span class="token builtin">UIView</span><span class="token punctuation">.</span><span class="token function">transition</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span> <span class="token keyword">self</span><span class="token punctuation">.</span>view<span class="token punctuation">,</span> duration<span class="token punctuation">:</span> <span class="token number">0.5</span><span class="token punctuation">,</span> options<span class="token punctuation">:</span> animationOption<span class="token punctuation">,</span> animations<span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token keyword">self</span><span class="token punctuation">.</span>view<span class="token punctuation">.</span>alpha <span class="token operator">=</span> <span class="token number">0.3</span><span class="token punctuation">}</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token number">_</span> <span class="token keyword">in</span>
					vc<span class="token punctuation">.</span>modalPresentationStyle <span class="token operator">=</span> <span class="token punctuation">.</span>overCurrentContext
					<span class="token keyword">self</span><span class="token punctuation">.</span><span class="token function">present</span><span class="token punctuation">(</span>vc<span class="token punctuation">,</span> animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span> completion<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">)</span>
				<span class="token punctuation">}</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
</div>
</body>

</html>
