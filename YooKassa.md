<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>YooKassa</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><ul>
<li><a href="%D1%81%D1%85%D0%B5%D0%BC%D0%B0-%D0%BF%D0%BB%D0%B0%D1%82%D0%B5%D0%B6%D0%B0">Схема платежа</a></li>
<li><a href="%D1%82%D0%B5%D1%80%D0%BC%D0%B8%D0%BD%D1%8B">Термины</a></li>
<li><a href="#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0">Установка</a></li>
<li><a href="#%D0%B8%D0%BD%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F">Инициализация</a></li>
<li><a href="#%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%BD%D0%B0%D1%8F-%D1%87%D0%B0%D1%81%D1%82%D1%8C-%D0%BD%D0%B0%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B0-%D0%BD%D0%B0-%D1%8F%D0%B7%D1%8B%D0%BA%D0%B5-php">Серверная часть написана на языке php</a></li>
</ul>
<h3 id="полезные-ссылки">Полезные ссылки</h3>
<ul>
<li><a href="https://yookassa.ru/developers/payments/sdk-tokens?lang=php">Документация YooKassa</a></li>
<li><a href="https://yookassa.ru/developers/api?lang=php#create_payment">Справочник YooKassa, примеры кода сервера</a></li>
</ul>
<h1 id="схема-платежа">Схема платежа</h1>
<p><img src="Components/YooKassa/YooKassa.png" alt="alt text" title="Описание будет тут"></p>
<h1 id="термины">Термины</h1>
<ul>
<li><strong>token</strong> - Получаемый ключ с YooKassa как альтернатива платежным данным.</li>
<li><strong>IdempotenceKey</strong> - Уникальный ключ который генерируется на стороне клиента при старте приложения и обновляется при получении статуса произведенного платежа. Ключ исключает создание дубликатов платежей при возникновении ошибок различного рода.</li>
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
<h3 id="импорт-библиотеки-yookassa">Импорт библиотеки YooKassa</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">import</span> <span class="token builtin">YooKassaPayments</span>
</code></pre>
<h3 id="объявление-свойств">Объявление свойств</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">final</span>  <span class="token keyword">let</span>  clientApplicationKey <span class="token operator">=</span> <span class="token string">"test_ODExMzkxT6xTXvpxnOTT4nVxxSK5vJTUMjL47pzIFYY"</span>  <span class="token comment">// Ключ приложения</span>
<span class="token keyword">final</span>  <span class="token keyword">let</span>  moneyAuthClientId <span class="token operator">=</span> <span class="token string">"idUser1"</span>  <span class="token comment">// Уникальный идентификатор пользователя, привязан к аккаунту</span>
<span class="token comment">// Отображаемые данные, но не действительные</span>
<span class="token keyword">let</span> shopName <span class="token operator">=</span> <span class="token string">"AliBaba"</span>  <span class="token comment">// Название магазина</span>
<span class="token keyword">let</span> amount <span class="token operator">=</span> <span class="token function">Amount</span><span class="token punctuation">(</span>value<span class="token punctuation">:</span> <span class="token number">999.99</span><span class="token punctuation">,</span> currency<span class="token punctuation">:</span> <span class="token punctuation">.</span>rub<span class="token punctuation">)</span> <span class="token comment">// Сумма и валюта покупки</span>
<span class="token keyword">let</span>  purchaseDescription <span class="token operator">=</span> <span class="token string">"Пакет гороха"</span>  <span class="token comment">// Описание покупки</span>
<span class="token keyword">var</span>  inputData<span class="token punctuation">:</span> <span class="token builtin">TokenizationFlow</span><span class="token operator">?</span>
</code></pre>
<h3 id="инициализация-во-viewdidload">Инициализация во viewDidLoad()</h3>
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
<h3 id="активация-начала-платежа">Активация начала платежа</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token atrule">@IBAction</span> <span class="token keyword">func</span> <span class="token function">buy</span><span class="token punctuation">(</span><span class="token number">_</span> sender<span class="token punctuation">:</span> <span class="token builtin">Any</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">guard</span> <span class="token keyword">let</span> inputData <span class="token operator">=</span> inputData <span class="token keyword">else</span> <span class="token punctuation">{</span><span class="token keyword">return</span><span class="token punctuation">}</span>
	<span class="token keyword">let</span> viewController <span class="token operator">=</span> <span class="token builtin">TokenizationAssembly</span><span class="token punctuation">.</span><span class="token function">makeModule</span><span class="token punctuation">(</span>inputData<span class="token punctuation">:</span> inputData<span class="token punctuation">,</span> moduleOutput<span class="token punctuation">:</span> <span class="token keyword">self</span><span class="token punctuation">)</span>
	<span class="token function">present</span><span class="token punctuation">(</span>viewController<span class="token punctuation">,</span> animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span> completion<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">)</span> <span class="token comment">// Отображается модальное окно выбора способа оплаты</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="расширения-обработки-событий">Расширения обработки событий</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">extension</span> <span class="token builtin">InitialViewController</span><span class="token punctuation">:</span> <span class="token builtin">TokenizationModuleOutput</span> <span class="token punctuation">{</span>
	<span class="token comment">// Будет вызван, когда процесс токенизации успешно пройдет.</span>
	<span class="token keyword">func</span> <span class="token function">tokenizationModule</span><span class="token punctuation">(</span><span class="token number">_</span> module<span class="token punctuation">:</span> <span class="token builtin">TokenizationModuleInput</span><span class="token punctuation">,</span> didTokenize token<span class="token punctuation">:</span> <span class="token builtin">Tokens</span><span class="token punctuation">,</span> paymentMethodType<span class="token punctuation">:</span> <span class="token builtin">PaymentMethodType</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token comment">// Отправьте токен в вашу систему</span>
		<span class="token keyword">let</span> model <span class="token operator">=</span> <span class="token function">Payment</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
		model<span class="token punctuation">.</span><span class="token function">sendPayment</span><span class="token punctuation">(</span>token<span class="token punctuation">:</span> token<span class="token punctuation">.</span>paymentToken<span class="token punctuation">,</span> idOrder<span class="token punctuation">:</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token punctuation">(</span>response<span class="token punctuation">,</span>error<span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">Void</span> <span class="token keyword">in</span>
			<span class="token comment">// Закрывает модальное окно токенизации</span>
			<span class="token builtin">DispatchQueue</span><span class="token punctuation">.</span>main<span class="token punctuation">.</span>async <span class="token punctuation">{</span> <span class="token punctuation">[</span><span class="token keyword">weak</span> <span class="token keyword">self</span><span class="token punctuation">]</span> <span class="token keyword">in</span>
				<span class="token keyword">guard</span> <span class="token keyword">let</span> <span class="token keyword">self</span> <span class="token operator">=</span> <span class="token keyword">self</span> <span class="token keyword">else</span> <span class="token punctuation">{</span> <span class="token keyword">return</span> <span class="token punctuation">}</span>
				<span class="token keyword">self</span><span class="token punctuation">.</span><span class="token function">dismiss</span><span class="token punctuation">(</span>animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">)</span>
			<span class="token punctuation">}</span>
			<span class="token keyword">if</span> <span class="token keyword">let</span> error <span class="token operator">=</span> error <span class="token punctuation">{</span>
				<span class="token function">print</span><span class="token punctuation">(</span>error<span class="token punctuation">)</span>
				<span class="token keyword">return</span>
			<span class="token punctuation">}</span>
			<span class="token keyword">guard</span> <span class="token keyword">let</span> status <span class="token operator">=</span> response<span class="token operator">?</span><span class="token punctuation">[</span><span class="token string">"status"</span><span class="token punctuation">]</span> <span class="token keyword">as</span><span class="token operator">?</span> <span class="token builtin">String</span> <span class="token keyword">else</span> <span class="token punctuation">{</span><span class="token keyword">return</span><span class="token punctuation">}</span>
			<span class="token keyword">switch</span> <span class="token punctuation">(</span>status<span class="token punctuation">)</span> <span class="token punctuation">{</span>
				<span class="token keyword">case</span> <span class="token string">"succeeded"</span><span class="token punctuation">:</span>
					<span class="token comment">// Вызов сообщения успешного платежа</span>
				<span class="token keyword">case</span> <span class="token string">"canceled"</span><span class="token punctuation">:</span>
					<span class="token comment">// Вызов сообщения отклоненного платежа</span>
				<span class="token keyword">default</span><span class="token punctuation">:</span>
					<span class="token function">print</span><span class="token punctuation">(</span><span class="token string">"defaultCase"</span><span class="token punctuation">)</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
	
	<span class="token comment">// Будет вызван, когда пользователь не завершил оплату и не завершил работу. Если пользователь выйдет не дождавшись окончания операции</span>
	<span class="token keyword">func</span> <span class="token function">didFinish</span><span class="token punctuation">(</span>on module<span class="token punctuation">:</span> <span class="token builtin">TokenizationModuleInput</span><span class="token punctuation">,</span> with error<span class="token punctuation">:</span> <span class="token builtin">YooKassaPaymentsError</span><span class="token operator">?</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token builtin">DispatchQueue</span><span class="token punctuation">.</span>main<span class="token punctuation">.</span>async <span class="token punctuation">{</span> <span class="token punctuation">[</span><span class="token keyword">weak</span> <span class="token keyword">self</span><span class="token punctuation">]</span> <span class="token keyword">in</span>
			<span class="token keyword">guard</span> <span class="token keyword">let</span> <span class="token keyword">self</span> <span class="token operator">=</span> <span class="token keyword">self</span> <span class="token keyword">else</span> <span class="token punctuation">{</span> <span class="token keyword">return</span> <span class="token punctuation">}</span>
			<span class="token keyword">self</span><span class="token punctuation">.</span><span class="token function">dismiss</span><span class="token punctuation">(</span>animated<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">)</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
	<span class="token comment">// Будет вызван, когда 3-D безопасный процесс успешно пройдет.</span>
	<span class="token keyword">func</span> <span class="token function">didSuccessfullyPassedCardSec</span><span class="token punctuation">(</span>on module<span class="token punctuation">:</span> <span class="token builtin">TokenizationModuleInput</span><span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
	<span class="token comment">// Будет вызван, когда процесс подтверждения успешно пройдет. Оплата через веб-клиент, статус pending</span>
	<span class="token keyword">func</span> <span class="token function">didSuccessfullyConfirmation</span><span class="token punctuation">(</span>paymentMethodType<span class="token punctuation">:</span> <span class="token builtin">PaymentMethodType</span><span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="модель">Модель</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">import</span> <span class="token builtin">Foundation</span>
<span class="token keyword">import</span> <span class="token builtin">Alamofire</span>
<span class="token keyword">import</span> <span class="token builtin">AlamofireObjectMapper</span>

<span class="token keyword">class</span>  <span class="token class-name">Payment</span> <span class="token punctuation">{</span>
	<span class="token keyword">func</span> <span class="token function">sendPayment</span><span class="token punctuation">(</span>token<span class="token punctuation">:</span> <span class="token builtin">String</span><span class="token punctuation">,</span> idOrder<span class="token punctuation">:</span> <span class="token builtin">Int</span><span class="token punctuation">,</span> completion<span class="token punctuation">:</span> @<span class="token function">escaping</span> <span class="token punctuation">(</span><span class="token number">_</span> response<span class="token punctuation">:</span> <span class="token builtin">NSDictionary</span><span class="token operator">?</span><span class="token punctuation">,</span> <span class="token number">_</span> error<span class="token punctuation">:</span>  <span class="token builtin">Error</span><span class="token operator">?</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">Void</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">guard</span> <span class="token keyword">let</span> url <span class="token operator">=</span> <span class="token function">URL</span><span class="token punctuation">(</span>string<span class="token punctuation">:</span> <span class="token string">"http://192.168.1.107:8000/"</span><span class="token punctuation">)</span> <span class="token keyword">else</span> <span class="token punctuation">{</span><span class="token keyword">return</span><span class="token punctuation">}</span>
		<span class="token keyword">let</span> param<span class="token punctuation">:</span> <span class="token builtin">Parameters</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
			<span class="token string">"idempotenceKey"</span><span class="token punctuation">:</span> <span class="token function">idempotenceKeyGenerator</span><span class="token punctuation">(</span>length<span class="token punctuation">:</span> <span class="token number">36</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
			<span class="token string">"paymentToken"</span><span class="token punctuation">:</span> token<span class="token punctuation">,</span>
			<span class="token string">"idOrder"</span><span class="token punctuation">:</span> idOrder
		<span class="token punctuation">]</span>
		<span class="token builtin">Alamofire</span><span class="token punctuation">.</span><span class="token function">request</span><span class="token punctuation">(</span>url<span class="token punctuation">,</span> method<span class="token punctuation">:</span> <span class="token punctuation">.</span>post<span class="token punctuation">,</span> parameters<span class="token punctuation">:</span> param<span class="token punctuation">,</span> encoding<span class="token punctuation">:</span> <span class="token builtin">URLEncoding</span><span class="token punctuation">.</span><span class="token keyword">default</span><span class="token punctuation">,</span> headers<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">)</span>
			<span class="token punctuation">.</span>responseJSON <span class="token punctuation">{</span> response <span class="token keyword">in</span>
			<span class="token keyword">switch</span> response<span class="token punctuation">.</span>result <span class="token punctuation">{</span>
				<span class="token keyword">case</span> <span class="token punctuation">.</span><span class="token function">success</span><span class="token punctuation">(</span><span class="token keyword">let</span> response<span class="token punctuation">)</span><span class="token punctuation">:</span>
				<span class="token keyword">let</span> response <span class="token operator">=</span> response <span class="token keyword">as</span><span class="token operator">!</span> <span class="token builtin">NSDictionary</span>
				<span class="token function">completion</span><span class="token punctuation">(</span>response<span class="token punctuation">,</span> <span class="token constant">nil</span><span class="token punctuation">)</span>
				<span class="token keyword">case</span> <span class="token punctuation">.</span><span class="token function">failure</span><span class="token punctuation">(</span><span class="token keyword">let</span> error<span class="token punctuation">)</span><span class="token punctuation">:</span>
				<span class="token function">completion</span><span class="token punctuation">(</span><span class="token constant">nil</span><span class="token punctuation">,</span> error<span class="token punctuation">)</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
	<span class="token keyword">func</span> <span class="token function">idempotenceKeyGenerator</span><span class="token punctuation">(</span>length<span class="token punctuation">:</span> <span class="token builtin">Int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">String</span> <span class="token punctuation">{</span>
		<span class="token keyword">let</span> letters <span class="token operator">=</span> <span class="token string">"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"</span>
		<span class="token keyword">return</span> <span class="token function">String</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token operator">&lt;</span>length<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token builtin">map</span><span class="token punctuation">{</span> <span class="token number">_</span> <span class="token keyword">in</span> letters<span class="token punctuation">.</span><span class="token function">randomElement</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token operator">!</span> <span class="token punctuation">}</span><span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h1 id="серверная-часть-написана-на-языке-php">Серверная часть написана на языке php</h1>
<h3 id="установка-библиотеки-yookassa-через-composer">Установка библиотеки YooKassa через Composer</h3>
<p>composer.json</p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
	<span class="token string">"require"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
		<span class="token string">"php"</span><span class="token punctuation">:</span> <span class="token string">"&gt;=5.3.2"</span><span class="token punctuation">,</span>
		<span class="token string">"yoomoney/yookassa-sdk-php"</span><span class="token punctuation">:</span> <span class="token string">"^2.1"</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="код-серверной-части">Код серверной части</h3>
<pre class=" language-php"><code class="prism  language-php"><span class="token php language-php"><span class="token delimiter important">&lt;?php</span>
	<span class="token keyword">require</span>  <span class="token constant">__DIR__</span>  <span class="token punctuation">.</span>  <span class="token string">'/vendor/autoload.php'</span><span class="token punctuation">;</span>

	<span class="token keyword">use</span> <span class="token package">YooKassa<span class="token punctuation">\</span>Client</span><span class="token punctuation">;</span>
	<span class="token variable">$client</span> <span class="token operator">=</span> <span class="token keyword">new</span>  <span class="token class-name">Client</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token variable">$client</span><span class="token operator">-</span><span class="token operator">&gt;</span><span class="token function">setAuth</span><span class="token punctuation">(</span><span class="token string">'811391'</span><span class="token punctuation">,</span> <span class="token string">'test_N-jp4quY-VGQg27blFQT5VI1_9YDMr5HL0udkeidwVM'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

	<span class="token comment">// Данные товара из БД, на основании idOrder</span>
	<span class="token comment">// $_POST["idOrder"];</span>
	<span class="token variable">$amountValue</span> <span class="token operator">=</span> <span class="token string">'2.00'</span><span class="token punctuation">;</span>
	<span class="token variable">$amountCurrency</span> <span class="token operator">=</span> <span class="token string">'RUB'</span><span class="token punctuation">;</span>
	<span class="token variable">$orderDescription</span> <span class="token operator">=</span> <span class="token string">'Зеленый горошек'</span><span class="token punctuation">;</span>

	<span class="token variable">$response</span> <span class="token operator">=</span> <span class="token variable">$client</span><span class="token operator">-</span><span class="token operator">&gt;</span><span class="token function">createPayment</span><span class="token punctuation">(</span>
		<span class="token keyword">array</span><span class="token punctuation">(</span>
			<span class="token string">'payment_token'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">"paymentToken"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
			<span class="token string">'amount'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token keyword">array</span><span class="token punctuation">(</span>
				<span class="token string">'value'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token variable">$amountValue</span><span class="token punctuation">,</span>
				<span class="token string">'currency'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token variable">$amountCurrency</span><span class="token punctuation">,</span>
			<span class="token punctuation">)</span><span class="token punctuation">,</span>
			<span class="token string">'capture'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token boolean">true</span><span class="token punctuation">,</span> <span class="token comment">// false - двухстадийный платёж</span>
			<span class="token string">'description'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token variable">$orderDescription</span><span class="token punctuation">,</span>
			<span class="token string">'metadata'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token keyword">array</span><span class="token punctuation">(</span>
			<span class="token string">'order_id'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">"idOrder"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
			<span class="token punctuation">)</span>
		<span class="token punctuation">)</span><span class="token punctuation">,</span>
		<span class="token function">uniqid</span><span class="token punctuation">(</span><span class="token variable">$_POST</span><span class="token punctuation">[</span><span class="token string">"idempotenceKey"</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token boolean">true</span><span class="token punctuation">)</span> <span class="token comment">// Уникальный ключ который запишется в БД</span>
	<span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token variable">$data</span> <span class="token operator">=</span> <span class="token keyword">array</span><span class="token punctuation">(</span>
	<span class="token string">"status"</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token variable">$response</span><span class="token operator">-</span><span class="token operator">&gt;</span><span class="token property">status</span>
	<span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">echo</span> <span class="token function">json_encode</span><span class="token punctuation">(</span> <span class="token variable">$data</span> <span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token delimiter important">?&gt;</span></span>
</code></pre>
</div>
</body>

</html>
