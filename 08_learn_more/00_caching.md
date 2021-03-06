# Caching

--------------------------------------------------------

* [Usage](#usage)
	- [Basics](#usage:basics)
	- [Magic shortcut](#usage:magic_shortcut)

--------------------------------------------------------

The cache library provides a simple and consistent interface to the most common caching solutions:

* APC
* APCU
* Database
* File
* Memcache / Memcached
* Memory
* Null
* Redis
* XCache
* ZendDisk
* ZendMemory
* WinCache

> The memory cache adapter is non-persistent and will be cleared between each request. The null adapter will not store any data.

--------------------------------------------------------

<a id="usage"></a>

### Usage

<a id="usage:basics"></a>

#### Basics

To get an instance of the default cache just call the ```CacheManager::instance``` method. If you want to get an instance of any of the other cache configurations defined in the config file then you'll have to pass it the configuration name.

	// Returns instance of the "default" cache configuration defined in the config file

	$cache = $this->cache->instance();

	// Returns instance of the "apc" cache configuration defined in the config file

	$cache = $this->cache->instance('apc');

Adding data to the cache is done using the ```put``` method. The method returns TRUE on success or FALSE on failure.

	$cache->put('my_array', [1, 2, 3, 4], 3600);

The ```get``` method is used to retrieve data from the cache. The method returns FALSE if the cached data has expired or if it is not found.

	$cached = $cache->get('my_array');


The ```getOrElse``` method returns the data if the key exists and caches the return value of the closure if it doesn't. The closure does not get executed if the key exists in the cache.

	$cached = $cache->getOrElse('foo', function()
	{
		sleep(5);

		return 'this will get cached for 30 seconds';
	}, 30);

You can check whether or not an item exists in the cache by using the ```has``` method.

	if($cache->has('foo'))
	{
		// Do something
	}

Removing data from the cache is done by using the ```remove``` method. The method returns TRUE on success or FALSE on failure.

	$cache->remove('my_array');

You can clear the entire cache by using the ```clear``` method. The method returns TRUE on success or FALSE on failure. Note that clearing the cache might also affect other applications.

	$cache->clear();

> Clearing the cache can affect other applications when using shared memory caching solutions such as APC and Memcache.

<a id="usage:magic_shortcut"></a>

#### Magic shortcut

You can access the default cache instance directly without having to go through the ```instance``` method thanks to the magic ```__call``` method.

	$cached = $this->cache->get('my_array');