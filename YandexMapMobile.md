<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>YandexMapMobile</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><ul>
<li><a href="#%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0">Установка</a></li>
<li><a href="#%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-viewcontroller">Использование  ViewController</a></li>
<li><a href="#%D1%81%D0%B2%D0%BE%D0%B9%D1%81%D1%82%D0%B2%D0%B0">Свойства</a></li>
<li><a href="#%D0%B2%D1%8B%D1%81%D1%82%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BF%D0%BE%D0%B7%D0%B8%D1%86%D0%B8%D0%B8-%D0%BE%D0%B1%D0%B7%D0%BE%D1%80%D0%B0-%D0%BA%D0%B0%D0%BC%D0%B5%D1%80%D1%8B">Выставление позиции обзора камеры</a></li>
<li><a href="#%D1%8D%D0%BB%D0%B5%D0%BC%D0%B5%D0%BD%D1%82%D1%8B-%D0%B8-%D1%81%D0%BB%D1%83%D1%88%D0%B0%D1%82%D0%B5%D0%BB%D0%B8">Элементы и слушатели</a>
<ul>
<li><a href="#%D0%BC%D0%B0%D1%80%D0%BA%D0%B5%D1%80-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8F">Маркер пользователя</a></li>
<li><a href="#%D0%BE%D0%B4%D0%BD%D0%BE%D0%BA%D1%80%D0%B0%D1%82%D0%BD%D0%BE%D0%B5-%D0%B8-%D0%B4%D0%BE%D0%BB%D0%B3%D0%BE%D0%B5-%D0%BD%D0%B0%D0%B6%D0%B0%D1%82%D0%B8%D0%B5-%D0%BD%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%83">Однократное и долгое нажатие на карту</a></li>
<li><a href="#%D0%BE%D0%B6%D0%B8%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B8-%D0%BA%D0%B0%D1%80%D1%82%D1%8B">Ожидание загрузки карты</a></li>
<li><a href="#%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BE%D0%BE%D1%80%D0%B4%D0%B8%D0%BD%D0%B0%D1%82-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8F-%D0%BF%D0%BE%D1%81%D0%BB%D0%B5-%D1%80%D0%B0%D0%B7%D1%80%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D1%8F">Получение координат пользователя после разрешения</a></li>
<li><a href="#%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BD%D0%BE%D0%B2%D1%8B%D1%85-%D0%BC%D0%B0%D1%80%D0%BA%D0%B5%D1%80%D0%BE%D0%B2">Добавление новых маркеров</a></li>
</ul>
</li>
</ul>
<h1 id="установка">Установка</h1>
<p>В консоли<br>
<code>pod install</code><br>
В файле ‘Podfile’<br>
<code>pod 'YandexMapsMobile', '4.0.0-lite'</code><br>
В консоли<br>
<code>pod update</code></p>
<p>В AppDelegate</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">import</span> <span class="token builtin">YandexMapsMobile</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">func</span> <span class="token function">application</span><span class="token punctuation">(</span><span class="token number">_</span> application<span class="token punctuation">:</span> <span class="token builtin">UIApplication</span><span class="token punctuation">,</span> didFinishLaunchingWithOptions launchOptions<span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token builtin">UIApplication</span><span class="token punctuation">.</span><span class="token builtin">LaunchOptionsKey</span><span class="token punctuation">:</span> <span class="token builtin">Any</span><span class="token punctuation">]</span><span class="token operator">?</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">Bool</span> <span class="token punctuation">{</span>

<span class="token builtin">YMKMapKit</span><span class="token punctuation">.</span><span class="token function">setApiKey</span><span class="token punctuation">(</span><span class="token builtin">Settings</span><span class="token punctuation">.</span>yandexAPIKey<span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">return</span> <span class="token boolean">true</span>
<span class="token punctuation">}</span>
</code></pre>
<p>В info.plist добавить два свойства</p>
<pre><code>Privacy - Location Always and When In Use Usage Description = someText
Privacy - Location When In Use Usage Description = someText // не обязательное
</code></pre>
<h1 id="использование-viewcontroller">Использование ViewController</h1>
<p>Импорт библиотеки Яндекс карт</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">import</span> <span class="token builtin">YandexMapsMobile</span>
<span class="token keyword">import</span> <span class="token builtin">CoreLocation</span>
</code></pre>
<p>Подключение карты, в xib создаем новый элемент View и указываем в инспекторе свойств Class = YMKMapView</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token atrule">@IBOutlet</span> <span class="token keyword">weak</span> <span class="token keyword">var</span> mapView<span class="token punctuation">:</span> <span class="token builtin">YMKMapView</span><span class="token operator">!</span>
</code></pre>
<h2 id="свойства">Свойства</h2>
<pre class=" language-swift"><code class="prism  language-swift">mapView<span class="token punctuation">.</span>mapWindow<span class="token punctuation">.</span><span class="token builtin">map</span>
</code></pre>

<table>
<thead>
<tr>
<th>Свойства</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr>
<td>.isRotateGesturesEnabled = false</td>
<td>Вращение карты, false - заблокировано</td>
</tr>
<tr>
<td>cameraPosition.zoom</td>
<td>Получает зум камеры, только getter</td>
</tr>
</tbody>
</table><h3 id="выставление-позиции-обзора-камеры">Выставление позиции обзора камеры</h3>
<p>targer - одна координата, типа YMKPoint<br>
zoom - масштам, 0 минимальный, 20 - уже видны здания<br>
azimuth - вращения карты прочив часовой стрелки в градусах<br>
tilt - угол наклона камеры в грудусах</p>
<pre class=" language-swift"><code class="prism  language-swift">mapView<span class="token punctuation">.</span>mapWindow<span class="token punctuation">.</span><span class="token builtin">map</span><span class="token punctuation">.</span><span class="token function">move</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span><span class="token function">YMKCameraPosition</span><span class="token punctuation">(</span>target<span class="token punctuation">:</span> <span class="token function">YMKPoint</span><span class="token punctuation">(</span>latitude<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span> longitude<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">,</span> zoom<span class="token punctuation">:</span> <span class="token number">14</span><span class="token punctuation">,</span> azimuth<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span> tilt<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<p>Улучшенная версия:</p>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token function">moveCamera</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token comment">// Рекомендуестся использовать после окончательной загрузки карты</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">func</span> <span class="token function">moveCamera</span><span class="token punctuation">(</span>lat<span class="token punctuation">:</span> <span class="token builtin">Double</span><span class="token punctuation">,</span> lon<span class="token punctuation">:</span> <span class="token builtin">Double</span><span class="token punctuation">,</span> zoom<span class="token punctuation">:</span> <span class="token builtin">Float</span> <span class="token operator">=</span> <span class="token number">14</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span> point <span class="token operator">=</span> <span class="token function">YMKPoint</span><span class="token punctuation">(</span>latitude<span class="token punctuation">:</span> lat<span class="token punctuation">,</span> longitude<span class="token punctuation">:</span> lon<span class="token punctuation">)</span>
	<span class="token keyword">let</span> position <span class="token operator">=</span> <span class="token function">YMKCameraPosition</span><span class="token punctuation">(</span>target<span class="token punctuation">:</span> point<span class="token punctuation">,</span> zoom<span class="token punctuation">:</span> zoom<span class="token punctuation">,</span> azimuth<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span> tilt<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">)</span>
	<span class="token keyword">let</span> animate <span class="token operator">=</span> <span class="token function">YMKAnimation</span><span class="token punctuation">(</span>type<span class="token punctuation">:</span> <span class="token punctuation">.</span>smooth<span class="token punctuation">,</span> duration<span class="token punctuation">:</span> <span class="token number">1.0</span><span class="token punctuation">)</span>
	<span class="token keyword">self</span><span class="token punctuation">.</span>mapView<span class="token punctuation">.</span>mapWindow<span class="token punctuation">.</span><span class="token builtin">map</span><span class="token punctuation">.</span><span class="token function">move</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span> position<span class="token punctuation">,</span> animationType<span class="token punctuation">:</span> animate<span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<h1 id="элементы-и-слушатели">Элементы и слушатели</h1>
<h3 id="маркер-пользователя">Маркер пользователя</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token comment">// Рекомендуестя использовать с locationManagerDidChangeAuthorization</span>
<span class="token function">setUserLocation</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token comment">// default: viewDidLoad</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">func</span>  <span class="token function">setUserLocation</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span> mapKit <span class="token operator">=</span> <span class="token builtin">YMKMapKit</span><span class="token punctuation">.</span><span class="token function">sharedInstance</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
	<span class="token keyword">let</span> userLocationLayer <span class="token operator">=</span> mapKit<span class="token punctuation">.</span><span class="token function">createUserLocationLayer</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span> mapView<span class="token punctuation">.</span>mapWindow<span class="token punctuation">)</span>
	<span class="token comment">// Включить отображение местоположения</span>
	userLocationLayer<span class="token punctuation">.</span><span class="token function">setVisibleWithOn</span><span class="token punctuation">(</span><span class="token boolean">true</span><span class="token punctuation">)</span>
	<span class="token comment">// Заблокировать вращение значка</span>
	userLocationLayer<span class="token punctuation">.</span>isHeadingEnabled <span class="token operator">=</span> <span class="token boolean">true</span>
	<span class="token comment">// Добавить слушателя</span>
	userLocationLayer<span class="token punctuation">.</span><span class="token function">setObjectListenerWith</span><span class="token punctuation">(</span><span class="token keyword">self</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token comment">// Слушатель пользовательского маркера</span>
<span class="token keyword">extension</span>  <span class="token builtin">YandexMapViewController</span><span class="token punctuation">:</span> <span class="token builtin">YMKUserLocationObjectListener</span> <span class="token punctuation">{</span>
<span class="token comment">// Срабатывает при добавлении нового местоположения</span>
<span class="token keyword">func</span> <span class="token function">onObjectAdded</span><span class="token punctuation">(</span>with view<span class="token punctuation">:</span> <span class="token builtin">YMKUserLocationView</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span> pinPlacemark <span class="token operator">=</span> view<span class="token punctuation">.</span>pin<span class="token punctuation">.</span><span class="token function">useCompositeIcon</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
	pinPlacemark<span class="token punctuation">.</span><span class="token function">setIconWithName</span><span class="token punctuation">(</span><span class="token string">"icon"</span><span class="token punctuation">,</span> image<span class="token punctuation">:</span> <span class="token function">UIImage</span><span class="token punctuation">(</span>named<span class="token punctuation">:</span> <span class="token string">"me"</span><span class="token punctuation">)</span><span class="token operator">!</span><span class="token punctuation">,</span>style<span class="token punctuation">:</span><span class="token function">YMKIconStyle</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>

<span class="token comment">// Срабатывает при удалении местоположения</span>
<span class="token keyword">func</span> <span class="token function">onObjectRemoved</span><span class="token punctuation">(</span>with view<span class="token punctuation">:</span> <span class="token builtin">YMKUserLocationView</span><span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>

<span class="token comment">// Срабатывает при обновлении местоположения</span>
<span class="token keyword">func</span>  <span class="token function">onObjectUpdated</span><span class="token punctuation">(</span>with view<span class="token punctuation">:</span> <span class="token builtin">YMKUserLocationView</span><span class="token punctuation">,</span> event<span class="token punctuation">:</span> <span class="token builtin">YMKObjectEvent</span><span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="однократное-и-долгое-нажатие-на-карту">Однократное и долгое нажатие на карту</h3>
<pre class=" language-swift"><code class="prism  language-swift">mapView<span class="token punctuation">.</span>mapWindow<span class="token punctuation">.</span><span class="token builtin">map</span><span class="token punctuation">.</span><span class="token function">addInputListener</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span> <span class="token keyword">self</span><span class="token punctuation">)</span> <span class="token comment">// viewDidLoad</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">extension</span>  <span class="token builtin">YandexMapViewController</span><span class="token punctuation">:</span> <span class="token builtin">YMKMapInputListener</span> <span class="token punctuation">{</span>
<span class="token comment">// Срабатывает при однократном нажатии на карту</span>
<span class="token keyword">func</span> <span class="token function">onMapTap</span><span class="token punctuation">(</span>with <span class="token builtin">map</span><span class="token punctuation">:</span> <span class="token builtin">YMKMap</span><span class="token punctuation">,</span> point<span class="token punctuation">:</span> <span class="token builtin">YMKPoint</span><span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>

<span class="token comment">// Срабатывает при длительном нажатии на карту</span>
<span class="token keyword">func</span> <span class="token function">onMapLongTap</span><span class="token punctuation">(</span>with <span class="token builtin">map</span><span class="token punctuation">:</span> <span class="token builtin">YMKMap</span><span class="token punctuation">,</span> point<span class="token punctuation">:</span> <span class="token builtin">YMKPoint</span><span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="ожидание-загрузки-карты">Ожидание загрузки карты</h3>
<pre class=" language-swift"><code class="prism  language-swift">mapView<span class="token punctuation">.</span>mapWindow<span class="token punctuation">.</span><span class="token builtin">map</span><span class="token punctuation">.</span><span class="token function">setMapLoadedListenerWith</span><span class="token punctuation">(</span><span class="token keyword">self</span><span class="token punctuation">)</span> <span class="token comment">// viewDidLoad</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">extension</span>  <span class="token builtin">YandexMapViewController</span><span class="token punctuation">:</span> <span class="token builtin">YMKMapLoadedListener</span> <span class="token punctuation">{</span>
	<span class="token keyword">func</span> <span class="token function">onMapLoaded</span><span class="token punctuation">(</span>with statistics<span class="token punctuation">:</span> <span class="token builtin">YMKMapLoadStatistics</span><span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="получение-координат-пользователя-после-разрешения">Получение координат пользователя после разрешения</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">let</span>  locationManager <span class="token operator">=</span> <span class="token function">CLLocationManager</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token function">getUserLocation</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token comment">// viewDidLoad</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">func</span>  <span class="token function">getUserLocation</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	locationManager<span class="token punctuation">.</span>delegate <span class="token operator">=</span> <span class="token keyword">self</span>
	locationManager<span class="token punctuation">.</span>desiredAccuracy <span class="token operator">=</span> <span class="token constant">kCLLocationAccuracyNearestTenMeters</span>
	locationManager<span class="token punctuation">.</span><span class="token function">startUpdatingLocation</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">extension</span>  <span class="token builtin">YandexMapViewController</span><span class="token punctuation">:</span> <span class="token builtin">CLLocationManagerDelegate</span> <span class="token punctuation">{</span>
	<span class="token keyword">func</span> <span class="token function">locationManager</span><span class="token punctuation">(</span><span class="token number">_</span> manager<span class="token punctuation">:</span> <span class="token builtin">CLLocationManager</span><span class="token punctuation">,</span> didChangeAuthorization status<span class="token punctuation">:</span> <span class="token builtin">CLAuthorizationStatus</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">guard</span> <span class="token keyword">let</span> coordinate<span class="token punctuation">:</span> <span class="token builtin">CLLocationCoordinate2D</span> <span class="token operator">=</span> manager<span class="token punctuation">.</span>location<span class="token operator">?</span><span class="token punctuation">.</span>coordinate <span class="token keyword">else</span> <span class="token punctuation">{</span> <span class="token keyword">return</span> <span class="token punctuation">}</span>
		<span class="token keyword">self</span><span class="token punctuation">.</span>userLocation <span class="token operator">=</span> <span class="token function">YMKPoint</span><span class="token punctuation">(</span>latitude<span class="token punctuation">:</span> coordinate<span class="token punctuation">.</span>latitude<span class="token punctuation">,</span> longitude<span class="token punctuation">:</span> coordinate<span class="token punctuation">.</span>longitude<span class="token punctuation">)</span>
		<span class="token keyword">if</span> status <span class="token operator">==</span> <span class="token punctuation">.</span>authorizedAlways <span class="token operator">||</span> status <span class="token operator">==</span> <span class="token punctuation">.</span>authorizedWhenInUse <span class="token punctuation">{</span>
			<span class="token keyword">if</span> <span class="token keyword">let</span> local <span class="token operator">=</span> <span class="token keyword">self</span><span class="token punctuation">.</span>userLocation <span class="token punctuation">{</span>
				<span class="token function">moveCamera</span><span class="token punctuation">(</span>lat<span class="token punctuation">:</span> local<span class="token punctuation">.</span>latitude<span class="token punctuation">,</span> lon<span class="token punctuation">:</span> local<span class="token punctuation">.</span>longitude<span class="token punctuation">)</span>
				<span class="token function">setUserLocation</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="добавление-новых-маркеров">Добавление новых маркеров</h3>
<pre class=" language-swift"><code class="prism  language-swift"><span class="token keyword">struct</span> <span class="token builtin">Place</span> <span class="token punctuation">{</span>
	<span class="token keyword">var</span> lat<span class="token punctuation">:</span>  <span class="token builtin">Double</span>
	<span class="token keyword">var</span> lng<span class="token punctuation">:</span>  <span class="token builtin">Double</span>
	<span class="token keyword">var</span> id<span class="token punctuation">:</span> <span class="token builtin">String</span>
	<span class="token keyword">init</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		lat <span class="token operator">=</span> <span class="token number">0</span>
		lng <span class="token operator">=</span> <span class="token number">0</span>
		id <span class="token operator">=</span> <span class="token string">""</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">let</span> places<span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token builtin">Place</span><span class="token punctuation">]</span>
<span class="token keyword">let</span> markerIcon <span class="token operator">=</span> <span class="token function">UIImage</span><span class="token punctuation">(</span>named<span class="token punctuation">:</span> <span class="token string">"marker"</span><span class="token punctuation">)</span>
<span class="token keyword">func</span>  <span class="token function">setIconMarkerStyle</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">YMKIconStyle</span><span class="token punctuation">{</span>
	<span class="token keyword">return</span> <span class="token function">YMKIconStyle</span><span class="token punctuation">(</span>anchor<span class="token punctuation">:</span> <span class="token function">CGPoint</span><span class="token punctuation">(</span>x<span class="token punctuation">:</span> <span class="token number">0.5</span><span class="token punctuation">,</span>y<span class="token punctuation">:</span><span class="token number">1</span><span class="token punctuation">)</span> <span class="token keyword">as</span> <span class="token builtin">NSValue</span><span class="token punctuation">,</span>
		rotationType<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		zIndex<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		flat<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		visible<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		scale<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">,</span>
		tappableArea<span class="token punctuation">:</span> <span class="token constant">nil</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token function">addMarkers</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token comment">// viewDidLoad</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token comment">// Создаем коллекцию маркеров</span>
<span class="token keyword">func</span> <span class="token function">addMarkers</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span> collection <span class="token operator">=</span> mapView<span class="token punctuation">.</span>mapWindow<span class="token punctuation">.</span><span class="token builtin">map</span><span class="token punctuation">.</span>mapObjects<span class="token punctuation">.</span><span class="token function">addClusterizedPlacemarkCollection</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span> <span class="token keyword">self</span><span class="token punctuation">)</span>
	<span class="token keyword">for</span> place <span class="token keyword">in</span> places <span class="token punctuation">{</span>
		<span class="token comment">// Добавляем маркер в коллекцию</span>
		<span class="token keyword">let</span> placeMark <span class="token operator">=</span> collection<span class="token punctuation">.</span><span class="token function">addPlacemark</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span> <span class="token function">YMKPoint</span><span class="token punctuation">(</span>latitude<span class="token punctuation">:</span> place<span class="token punctuation">.</span>lat<span class="token punctuation">,</span> longitude<span class="token punctuation">:</span> place<span class="token punctuation">.</span>lng<span class="token punctuation">)</span><span class="token punctuation">,</span> image<span class="token punctuation">:</span> markerIcon<span class="token punctuation">,</span> style<span class="token punctuation">:</span> <span class="token function">setIconMarkerStyle</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
		<span class="token comment">// Добавляем слушателя</span>
		placeMark<span class="token punctuation">.</span><span class="token function">addTapListener</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span> <span class="token keyword">self</span><span class="token punctuation">)</span>
		<span class="token comment">// Добавляем новые значения маркеру по ключу userData</span>
		placeMark<span class="token punctuation">.</span>userData <span class="token operator">=</span> place
	<span class="token punctuation">}</span>
	<span class="token comment">// Устанавливаем радиус и зумм группировки маркеров в кластер</span>
	collection<span class="token punctuation">.</span><span class="token function">clusterPlacemarks</span><span class="token punctuation">(</span>withClusterRadius<span class="token punctuation">:</span> <span class="token number">60</span><span class="token punctuation">,</span> minZoom<span class="token punctuation">:</span> <span class="token number">15</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
<span class="token keyword">extension</span>  <span class="token builtin">YandexMapViewController</span><span class="token punctuation">:</span> <span class="token builtin">YMKClusterListener</span><span class="token punctuation">,</span> <span class="token builtin">YMKClusterTapListener</span><span class="token punctuation">,</span> <span class="token builtin">YMKMapObjectTapListener</span> <span class="token punctuation">{</span>
	<span class="token comment">// Добавление изображения и слушателя кластеру</span>
	<span class="token keyword">func</span> <span class="token function">onClusterAdded</span><span class="token punctuation">(</span>with cluster<span class="token punctuation">:</span> <span class="token builtin">YMKCluster</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		cluster<span class="token punctuation">.</span>appearance<span class="token punctuation">.</span><span class="token function">setIconWith</span><span class="token punctuation">(</span>markerIcon<span class="token punctuation">,</span> style<span class="token punctuation">:</span> <span class="token function">setIconMarkerStyle</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
		cluster<span class="token punctuation">.</span><span class="token function">addClusterTapListener</span><span class="token punctuation">(</span>with<span class="token punctuation">:</span> <span class="token keyword">self</span><span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
	<span class="token comment">// Слушатель кластера</span>
	<span class="token keyword">func</span> <span class="token function">onClusterTap</span><span class="token punctuation">(</span>with cluster<span class="token punctuation">:</span> <span class="token builtin">YMKCluster</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">Bool</span> <span class="token punctuation">{</span>
		<span class="token comment">// Получаем данные случайного первого маркера из массива кластеров</span>
		<span class="token keyword">let</span> data <span class="token operator">=</span> cluster<span class="token punctuation">.</span>placemarks<span class="token punctuation">.</span><span class="token builtin">first</span><span class="token operator">?</span><span class="token punctuation">.</span>userData <span class="token keyword">as</span><span class="token operator">!</span> <span class="token builtin">Place</span>
		<span class="token function">moveCamera</span><span class="token punctuation">(</span>lat<span class="token punctuation">:</span> data<span class="token punctuation">.</span>lat<span class="token punctuation">,</span> lon<span class="token punctuation">:</span> data<span class="token punctuation">.</span>lng<span class="token punctuation">)</span>
		<span class="token keyword">return</span>  <span class="token boolean">true</span>
	<span class="token punctuation">}</span>
	<span class="token comment">// Слушатель маркера</span>
	<span class="token keyword">func</span> <span class="token function">onMapObjectTap</span><span class="token punctuation">(</span>with mapObject<span class="token punctuation">:</span> <span class="token builtin">YMKMapObject</span><span class="token punctuation">,</span> point<span class="token punctuation">:</span> <span class="token builtin">YMKPoint</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">Bool</span> <span class="token punctuation">{</span>
	<span class="token comment">// Получаем данные маркера</span>
	<span class="token keyword">let</span> data <span class="token operator">=</span> mapObject<span class="token punctuation">.</span><span class="token function">value</span><span class="token punctuation">(</span>forKey<span class="token punctuation">:</span> <span class="token string">"userData"</span><span class="token punctuation">)</span> <span class="token keyword">as</span><span class="token operator">!</span> <span class="token builtin">Place</span>
	<span class="token function">moveCamera</span><span class="token punctuation">(</span>lat<span class="token punctuation">:</span> data<span class="token punctuation">.</span>lat<span class="token punctuation">,</span> lon<span class="token punctuation">:</span> data<span class="token punctuation">.</span>lng<span class="token punctuation">)</span>
	<span class="token keyword">return</span>  <span class="token boolean">true</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
</div>
</body>

</html>
