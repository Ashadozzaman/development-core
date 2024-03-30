### Cache/Redis is very nesecary for big data project

- If we want use cache like file,database,redis
- For redis
```CACHE_DRIVER = redis //in env```
```
$users = Cache::remember('users', $minutes, function () {
   		 return DB::table('users')->get();
	});
```
THAT'S IT