**Service**:- laravel default service, if need we create own service, service actualy use for if need something use for every here in project.
create service like: `view()->share('name-service',$passdata);` it's call in boot() function under created provider.

**Container:** laravel buliding tool, Container manage service object in the project...manage defendency injuction...via setter,constuctor
- container register in register() function
- when we something register , laravel register return object->this object we use our full project anywhere.

(container basically object create kore, if service depend class/api, container manage this)

```
using view()->composer('file',function($view){
	$view()->with(User::all());
})
```


### Defendency Injuction//Class Defendency

if any class using __contucutor get another class object, this is class dependency.(ek class under anoth er class pass as a arrguments)

- Facade:: facade provide static interface in hole project
- EventListener:one event more then one listerner....specifiq time notify user
	- first event create
		- listener create
	- then evertServiceProvider register event $ listener

- Observer: Observer are used to group event listener for model.
- QueueJob:
	- make queue:table
	- migrate
	- ...implement shouldQueue
- TaskSheduler
- Login Authentication with OTP
- Get excel field data maatwebsite/excel
- Work with laravel October cms

### Dir Permission
Stroge  //   boostrap/cache
permission : sudo chmod -R 755


`Note: UUIDs are universally unique alpha-numeric identifiers`

### Get Duplicate value 
$duplicates = YourModel::select('column1', 'column2', 'column3')
    ->groupBy('column1', 'column2', 'column3')
    ->havingRaw('COUNT(*) > 1')
    ->get();
