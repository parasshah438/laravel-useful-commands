<!DOCTYPE html>
<html>
<head>
</head>
<body>
<h1>Laravel useful Commands</h1>

<h4>Route list</h4>
<pre>
	php artisan route:list
	
	Hide routes defined by third-party packages
	php artisan route:list --except-vendor
</pre>

<h4>Router HTTP Methods</h4>
<pre>
	Route::get($uri, $callback);
	Route::post($uri, $callback);
	Route::put($uri, $callback);
	Route::patch($uri, $callback);
	Route::delete($uri, $callback);
	Route::options($uri, $callback);	


	Multiple HTTP methods
	Route::methods(['GET', 'POST'], $uri, $callback);

	All HTTP methods
	Route::match(['GET', 'POST'], $uri, $callback);

	All HTTP methods
	Route::any($uri, $callback);

	All HTTP methods
	Route::allMethods($uri, $callback);
</pre>

<h4>Route Optional Parameters</h4>
<pre>
	Route::get('/user/{name?}', function ($name = null) {
		return $name;
	});
	
	Route::get('/user/{name?}', function ($name = 'John') {
		return $name;
	});
</pre>

<h4>Regular Expression Constraints</h4>
<pre>
	Route::get('/user/{name}', function ($name) {
		//
	})->where('name', '[A-Za-z]+');
	
	Route::get('/user/{id}', function ($id) {
		//
	})->where('id', '[0-9]+');
	
	Route::get('/user/{id}/{name}', function ($id, $name) {
		//
	})->where(['id' => '[0-9]+', 'name' => '[a-z]+']);
	
	Route::get('/user/{id}/{name}', function ($id, $name) {
		//
	})->whereInteger('id');
	
	Route::get('/user/{id}/{name}', function ($id, $name) {
		//
	})->whereAlpha('name');
</pre>

<h4>Accessing current route</h4>
<pre>
	$route = Route::current();
	$route = Route::currentRouteName();
	$route = Route::currentRouteAction();
</pre>

<h4>Redirect Routes</h4>
<pre>

	Route::redirect('/here', '/there');
	Route::redirect('/here', '/there', 301);
	Route::redirect('/here', '/there', 301, ['id' => 123]);
	Route::permanentRedirect('/here', '/there');

	php artisan route:list --redirect
	php artisan route:list --redirect --except-vendor
	php artisan route:list --redirect --only-vendor
	php artisan route:list --redirect --except-vendor --only-vendor
	php artisan route:list --redirect --only-vendor --except-vendor

	php artisan route:list --redirect --only=home
	php artisan route:list --redirect --except=home
	php artisan route:list --redirect --only=home --except=home

</pre>
<h4>Controller</h4>
<pre> 
	  php artisan make:controller UserController
	  php artisan make:controller UserController --model
	  php artisan make:controller UserController --model=User --resource
	  php artisan make:controller UserController --model=User --api
	  php artisan make:controller UserController --model=User --invokable
	  php artisan make:controller UserController --model=User --resource --api
	  php artisan make:controller UserController --model=User --resource --api --invokable
	  php artisan make:controller UserController --model=User --api --invokable
	  php artisan make:controller UserController --model=User --api --invokable --resource
	  php artisan make:controller UserController --model=User --api --invokable --resource --force
	  php artisan make:controller UserController --model=User --api --invokable --force
	  php artisan make:controller UserController --model=User --api --invokable --force --resource
	  php artisan make:controller UserController --resource  
	  php artisan make:controller UserController --api  
	  php artisan make:controller UserController --invokable 
	  php artisan make:controller UserController --model=Photo 
</pre> 

<h4>Model </h4>
<pre> 
	php artisan make:model Photo
	php artisan make:model Photo --migration --controller --resource 
	php artisan make:model Photo -crm
	php artisan make:model Photo --force
	php artisan make:model Photo --table=photos
	php artisan make:model Photo --table=photos --force
	php artisan make:model Photo --table=photos --connection=mysql
	php artisan make:model Photo --table=photos --connection=mysql --force
	php artisan make:model Photo --table=photos --connection=mysql --migration --force
	php artisan make:model Photo --table=photos --connection=mysql --migration --controller --resource --force
	php artisan make:model Photo --table=photos --connection=mysql --migration --controller --resource --force --preserve
	php artisan make:model Photo --table=photos --connection=mysql --migration --controller --resource --force --preserve --softdelete
	php artisan make:model Photo --table=photos --connection=mysql --migration --controller --resource --force --preserve --softdelete --timestamp
	php artisan make:model Photo --table=photos --connection=mysql --migration --controller --resource --force --preserve --softdelete --timestamp --with-comments
	php artisan make:model Photo --table=photos --connection=mysql --migration --controller --resource --force --preserve --softdelete --timestamp --with-comments --with-pivot
	php artisan make:model Photo --table=photos --connection=mysql --migration --controller --resource --force --preserve --softdelete --timestamp --with-comments --with-pivot --softdelete
	php artisan make:model Photo --table=photos --connection=mysql --migration --controller --resource --force --preserve --softdelete --timestamp --with-comments --with-pivot --softdelete --timestamp
</pre> 

<h4>Models - Mass assignment</h4>
<pre>
	protected $guarded = []; // Empty means all attributes are guarded

	protected $fillable = ['name', 'email'];

	protected $hidden = ['password', 'remember_token'];

	protected $casts = [
		'email_verified_at' => 'datetime',
	];

	protected $dates = ['deleted_at'];

	protected $with = ['posts'];

	protected $withCount = ['posts'];

	protected $appends = ['full_name'];
</pre>

<h4>Migration  </h4>
<pre> 
	Run the new migrations
	php artisan migrate	

	Rollback latest migration
	php artisan migrate:rollback

	Rollback all migrations
	php artisan migrate:reset

	Rollback all and re-migrate
	php artisan migrate:refresh

	Rollback all, re-migrate and run all seeders
	php artisan migrate:refresh --seed

	Create a migration
	php artisan make:migration create_users_table

	Create a migration with specified table
	php artisan make:migration create_users_table --table=users

	Create a migration with specified columns
	php artisan make:migration create_users_table --table=users --columns="name:string(255),email:string(255),password:string(255)"
	php artisan make:migration create_users_table --table=users --columns="name:string(255),email:string(255),password:string(255)" --create=users
</pre> 


<h4>Models - CRUD Operations</h4>
<pre>
	Create
	$newUser = User::create(['name' => 'John Doe', 'email' => 'john@example.com']);

	Update
	$user = User::find(1);
	$user->update(['name' => 'Updated Name']);
	User::where('status', 'inactive')->update(['status' => 'active']);

	Read
	$users = User::all();
	$user = User::find(1);
	$activeUsers = User::where('status', 'active')->get();
	$tags = Product::where('name', 'Some Product')->first()->tags;

	Delete
	$user = User::find(1);
	$user->delete();
	User::where('status', 'inactive')->delete();
</pre>
<h4>Seeder   </h4>
<pre> 
	php artisan make:seeder BooksTableSeeder
	php artisan make:seeder BooksTableSeeder --class=BooksTableSeeder
	php artisan make:seeder BooksTableSeeder --class=BooksTableSeeder --force
	php artisan make:seeder BooksTableSeeder --class=BooksTableSeeder --database=mysql
	php artisan make:seeder BooksTableSeeder --class=BooksTableSeeder --database=mysql --force
	php artisan make:seeder BooksTableSeeder --class=BooksTableSeeder --database=mysql --force --class=BooksTableSeeder
	php artisan make:seeder BooksTableSeeder --class=BooksTableSeeder --database=mysql --force --class=BooksTableSeeder --force
	php artisan make:seeder BooksTableSeeder --class=BooksTableSeeder --database=mysql --force --class=BooksTableSeeder --force --class=BooksTableSeeder

	php artisan db:seed
	php artisan db:seed --class=BooksTableSeeder
	php artisan db:seed --class=BooksTableSeeder --force
	php artisan db:seed --class=BooksTableSeeder --database=mysql
	php artisan db:seed --class=BooksTableSeeder --database=mysql --force
	php artisan db:seed --class=BooksTableSeeder --database=mysql --force --class=BooksTableSeeder

</pre> 

<h4>Request    </h4>
<pre> 
	php artisan make:request StoreBlogPost  
</pre> 

<h4>Middleware     </h4>
<pre> 
	php artisan make:middleware IsAdmin   
</pre> 

<h4>Policy      </h4>
<pre> 
	php artisan make:policy PostPolicy
	php artisan make:policy PostPolicy --model=Photo     
</pre> 

<h4>Command       </h4>
<pre> 
	php artisan make:command SendEmails 
	php artisan make:command SendEmails --command=Command      
</pre> 

<h4>Event        </h4>
<pre> 
	php artisan make:event OrderShipped     
</pre> 

<h4>Job         </h4>
<pre> 
	php artisan make:job SendReminderEmail    
	php artisan make:job SendReminderEmail --sync 
</pre> 

<h4>Listener          </h4>
<pre> 
	php artisan make:listener SendShipmentNotification     
	php artisan make:listener SendShipmentNotification --event=Event 
	php artisan make:listener SendShipmentNotification --queued 
</pre> 


<h4>Mail           </h4>
<pre> 
	php artisan make:mail OrderShipped     
	php artisan make:mail OrderShipped --markdown  
	php artisan make:mail OrderShipped --force 
</pre> 

<h4>Notification            </h4>
<pre> 
	php artisan make:notification InvoicePaid      
	php artisan make:notification InvoicePaid --markdown  
	php artisan make:notification InvoicePaid --force 
</pre> 

<h4>Provider             </h4>
<pre> 
	php artisan make:provider DuskServiceProvider  
</pre>

<h4>Test              </h4>
<pre> 
	php artisan make:test UserTest
	php artisan make:test UserTest --unit    
</pre> 

<h4>Channel               </h4>
<pre> 
	php artisan make:channel OrderChannel  
</pre> 

<h4>Exception                </h4>
<pre> 
	php artisan make:exception UserNotFoundException
	php artisan make:exception UserNotFoundException --render
	php artisan make:exception UserNotFoundException --report     
</pre> 

<h4>Factory                 </h4>
<pre> 
	php artisan make:factory PostFactory 
	php artisan make:factory PostFactory --model=Post     
</pre> 

<h4>Observer                  </h4>
<pre> 
	php artisan make:observer PostObserver  
	php artisan make:observer PostObserver --model=Post    
</pre> 

<h4>Rule</h4>
<pre> 
	php artisan make:rule Uppercase 
</pre> 

<h4>Resource</h4>
<pre> 
	php artisan make:resource PostResource
	php artisan make:resource PostResource --collection=Post  
</pre> 

<h4>Application overview</h4>
<pre> 
	php artisan about
	php artisan about --only=environment 
</pre>

<h4>Application maintenance mode</h4>
<pre> 
	php artisan down
	php artisan down --retry=60 (seconds)
	php artisan down --render="maintenance" (page)
	php artisan down --redirect=/
	php artisan down --secret="myapp"
	php artisan up
</pre>


<h4>HTTP Client</h4>
<pre>
	http Client
	php artisan http client
	php artisan http client --name=laravel
	php artisan http client --url=https://laravel.com
	php artisan http client --url=https://laravel.com --name=laravel

	$response = Http::get('https://api.quotable.io/random');

	$result = $response->json();
	$result = $response->object();
	$result = $response->collect();
	$result = $response->array();
	$result = $response->body();
	$result = $response->dump();
	$result = $response->download();
	$result = $response->plain();
	$result = $response->text();
	$result = $response->throw();
	$result = $response->status();
	$result = $response->successful();
	$result = $response->redirect();
	$result = $response->retry();
	$result = $response->retryAfter();
	$result = $response->headers();
	$result = $response->cookies();
	$result = $response->baseResponse();
	
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value']);
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->json();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->object();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->collect();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->array();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->body();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->dump();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->dump();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->download();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->plain();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->text();
	$response = Http::get('https://api.quotable.io/random', ['param' => 'value'])->throw();

</pre>

<h4>Authentication</h4>
<pre>
	Authentication
	php artisan make:auth
	php artisan make:auth --provider
	php artisan make:auth --provider --model=User
	php artisan make:auth --provider --model=User --table=users
	
	$user = auth()->user();
	$user = Auth::user();
	$user = Auth::id();
	$user = Auth::check();
	$user = Auth::guest();
	$user = Auth::user();

	$name = auth()->user()->name;
	$name = Auth::user()->name;
	$name = Auth::id()->name;
	$name = Auth::check()->name;
	$name = Auth::guest()->name;

	Only visible for guests and NOT for authenticated users (= not logged in)	
	@guest
	@endguest

	Only visible for authenticated users and NOT for guests (= logged in)
	@auth
	@endauth	
</pre>

<h4>Carbon</h4>
<pre>
	Import Carbon
	use Carbon\Carbon;

	$now = Carbon::now();
	$now = Carbon::now('Asia/Kolkata');
	$now = Carbon::now('Europe/London');
	$now = Carbon::now('America/New_York');
	$now = Carbon::now('America/Chicago');
	$now = Carbon::now('America/Denver');
	$now = Carbon::now('America/Los_Angeles');
	$now = Carbon::now('America/Sao_Paulo');
	$now = Carbon::now('Asia/Tokyo');
	$now = Carbon::now('Asia/Shanghai');
	$now = Carbon::now('Australia/Sydney');
	$now = Carbon::now('Pacific/Auckland');

	Current date and time
	$now = Carbon::now();
	echo $now; // 2024-06-27 12:00:00

	Specific date and time
	$newYear = Carbon::create(2024, 1, 1, 0, 0, 0);
	echo $newYear; // 2024-01-01 00:00:00

	Parse a date string
	$date = Carbon::parse('2024-06-27 12:00:00');
	echo $date; // 2024-06-27 12:00:00

	Create from timestamp
	$timestamp = Carbon::createFromTimestamp(1622499200);
	echo $timestamp; // 2021-06-01 12:00:00

	Add time
	echo $now->addDays(5); // 5 days from now
	echo $now->addWeeks(2); // 2 weeks from now
	echo $now->addMonths(3); // 3 months from now

	Subtract time
	echo $now->subDays(5); // 5 days ago
	echo $now->subWeeks(2); // 2 weeks ago
	echo $now->subMonths(3); // 3 months ago

	Start and end of periods
	echo $now->startOfDay(); // Start of today
	echo $now->endOfDay(); // End of today
	echo $now->startOfMonth(); // Start of the month
	echo $now->endOfMonth(); // End of the month


	Format date
	echo $now->format('Y-m-d H:i:s'); // 2024-06-27 12:00:00
	echo $now->toDateString(); // 2024-06-27
	echo $now->toFormattedDateString(); // Jun 27, 2024
	echo $now->toTimeString(); // 12:00:00
	echo $now->toDateTimeString(); // 2024-06-27 12:00:00

	Custom formats
	echo $now->format('l jS \\of F Y h:i:s A'); // Wednesday 27th of June 2024 12:00:00 PM

	$tomorrow = Carbon::tomorrow();
	if ($now->lt($tomorrow)) {
		echo 'Now is before tomorrow';
	}
	if ($now->gt($tomorrow)) {
		echo 'Now is after tomorrow';
	}
	if ($now->eq($tomorrow)) {
		echo 'Now is equal to tomorrow';
	}
	Checking if dates are the same day
	$anotherDate = Carbon::create(2024, 6, 27, 15, 0, 0);
	if ($now->isSameDay($anotherDate)) {
		echo 'Same day';
	}

	Human-readable dates
	echo $now->diffForHumans(); // 1 second ago
	echo $now->addDays(5)->diffForHumans(); // 5 days from now
	echo $now->subDays(5)->diffForHumans(); // 5 days ago

	Carbon::setLocale('fr');
	echo $now->diffForHumans(); // il y a 1 seconde

	Carbon::setLocale('es');
	echo $now->diffForHumans(); // hace 1 segundo

	Carbon::setLocale('fr');
	echo $now->diffForHumans(); // il y a 1 seconde

	Carbon::setLocale('es');
	echo $now->diffForHumans(); // hace 1 segundo

	$now = Carbon::now('America/New_York');
	echo $now; // Current time in New York

	$now = Carbon::now('Asia/Tokyo');
	echo $now; // Current time in Tokyo

	Convert timezone
	$nowInUtc = $now->setTimezone('UTC');
	echo $nowInUtc; // Convert current time to UTC

	$now = Carbon::now();
	Modify dates
	echo $now->addYears(1); // Add 1 year
	echo $now->subYears(2); // Subtract 2 years
	echo $now->addHours(3); // Add 3 hours
	echo $now->subMinutes(30); // Subtract 30 minutes

	To JSON
	echo $now->toJson(); // "2024-06-27T12:00:00.000000Z"

	From JSON
	$dateFromJson = Carbon::parse(json_decode('"2024-06-27T12:00:00.000000Z"'));
	echo $dateFromJson; // 2024-06-27 12:00:00

	Get today's date
	$today = Carbon::today();
	echo $today; // 2024-06-27 00:00:00

	Get yesterday's date
	$yesterday = Carbon::yesterday();
	echo $yesterday; // 2024-06-26 00:00:00

	Get tomorrow's date
	$tomorrow = Carbon::tomorrow();
	echo $tomorrow; // 2024-06-28 00:00:00

	Checking if date is in the past or future
	if ($now->isPast()) {
		echo 'The date is in the past';
	}

	if ($now->isFuture()) {
		echo 'The date is in the future';
	}

	Checking day of the week
	if ($now->isMonday()) {
		echo 'Today is Monday';
	}

	Age calculation
	$birthDate = Carbon::createFromDate(2000, 6, 27);
	echo $birthDate->age; // 24
</pre>

<h4>Blade - Directives</h4>
<pre>
	@dump($perPage, $newGenre, $genres->toArray())  
	@dd($perPage, $newGenre, $genres->toArray())

	If Statement
	@if($user->isAdmin)
    
	@else

	@endif

	Switch Statement
	@switch($role)
	@case('admin')
		@break
	@case('user')
		@break
	@default
	@endswitch

	Check if defined and not null
	@isset($products)
	@endisse

	Check if empty
	@empty($records)
	@endempty

	For loop
	@for ($i = 0; $i < 10; $i++)
    	{{ $i }}
	@endfor

	Foreach loop
	@foreach($products as $product)
		{{ $product->name }}
	@endforeach

	Forelse loop
	@forelse($products as $product)
		{{ $product->name }}
	@empty
		No products found
	@endforelse

	While loop
	@while (true)
	@endwhile

	Determine if a user is authenticated or not.
	@auth
	@endauth

	@guest
	@endguest

	Add raw php code
	@php
		$counter = 1;
	@endphp

	Show JSON data
	<pre>@json($products, JSON_PRETTY_PRINT)</pre>
</pre>

<h4>Publish the lang Folder in Laravel 11</h4>
<pre> 
	php artisan lang:publish
	php artisan lang:publish --existing
</pre>

<h4>Publish Config Files in Laravel 11</h4>
<pre> 
	php artisan config:publish
	php artisan config:publish --all
</pre>

<h4>Publish the various route files in Laravel 11</h4>
<pre> 
	php artisan install:api
	php artisan install:broadcasting
</pre>

<h1>Laravel Old Authentication (Artisan Command)</h1>
<p>composer create-project laravel/laravel my-app</p>
<p>php artisan make:auth</p>
<br>

<h1>Laravel New Authentication (Artisan Command)</h1>
<p>composer create-project laravel/laravel my-app</p>
<p>composer require laravel/ui</p> 
<p>composer require laravel/ui --dev</p>

<p> > php artisan ui --help </p>
<p>php artisan ui vue</p>
<p>php artisan ui react</p>
<p>php artisan ui bootstrap</p>

<p> > auth </p>
<p>php artisan ui vue --auth </p>
<p>php artisan ui react --auth</p>
<p>php artisan ui bootstrap --auth</p>

<p> > node</p>
<p>npm install</p>
<p>npm run dev</p>
<p>Compiling Assets (Mix)</p>
<p>npm run watch</p><br>
<p>Asset Bundling (Vite)</p>
<p>npm run build</p>
</body>
</html>
