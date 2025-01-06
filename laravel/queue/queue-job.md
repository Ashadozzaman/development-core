## Laravel queue able to set piority

**Senario:**
If you sending 2000 mail in queue at time need to send OTP meg this OTP is you first piority, that momunt you should set piority `high` for OTP.

```
// Call queue job
dispatch(new SendOTPJob())->onQueue('high')
// Command to run
php artisan queue:work --queue=high,default
```

### After Job Fail, how to get this or how notify fail queue

```
// App/Job/Job.php
public function failed($exception){
    Mail::send([],[],function($msg){
        $msg->to('admin@mail.com')
        ->subject('Job Fail')
        ->html('You this job fail');
    })
}
```

### Globally:

Set the global max attempts and retry delay in the queue worker:

```
php artisan queue:work --tries=5 --delay=30
```
