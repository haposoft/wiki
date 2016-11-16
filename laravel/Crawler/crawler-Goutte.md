1. Cài đặt Laravel

2. Cài đặt thư viện Goutte dùng để crawler

	Sơ qua về Goutte: Goutte được kế thừa và xây dựng trên những thư viện như Symfony BrowserKit và Guzzle, được viết và duy trì bởi @fabpot - founder của Symfony

	[1] dùng Terminal chạy lệnh: composer require fabpot/goutte

	[2] Khởi tạo 1 Goutte Client:
	use Goutte\Client;
	$client = new Client();

	[3] Gửi request với phương thức request():
	$crawler = $client->request('GET','https://crowdworks.jp/public/jobs/sgroup/2');

	[5 ] Filter 1 thẻ HTML: thẻ a với class = bottom
	$page = $crawler->filter('a.bottom')->attr('href');

	[ 6] Kiểm tra xem selector có tồn tại hay không:
	$hasTitle = count($crawler->filter('b.employer_name')) > 0;
	Có thể kiểm tra nhiều Selector để tránh lỗi ko tìm thấy 
	$title = $crawler->filter('.title, h2.heading')->text();

	[7 ] Click vào một button
	$crawler = $client->request('GET', 'https://github.com/');
	$crawler = $client->click($crawler->selectLink('Sign in')->link());
	$form = $crawler->selectButton('Sign in')->form();

3. Mọi người có thể đọc thêm ở đây về cách sử dụng 
https://symfony.com/doc/current/components/dom_crawler.html