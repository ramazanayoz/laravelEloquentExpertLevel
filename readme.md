

### Defining Relationship
 - [One To One](#one-to-one) 
 - [One To Many](#one-to-many) 
 - [Many To Many](#many-to-many) 
	 - [Retrieving Intermediate Table Columns](#retrieving-intermediate-table-columns)
	 - [Customizing The pivot Attribute Name](#customizing-the-pivot-attribute-name)
	 - [Filtering Relationships Via Intermediate Table Columns](#filtering-relationships-via-intermediate-table-columns)
- [Defining Custom Intermediate Table Models](#defining-custom-intermediate-table-models)
  - [Custom Pivot Models And Incrementing IDs](#custom-pivot-models-and-incrementing-ids)
- [Has One Through](#has-one-through)
 - [Has Many Through](#has-many-through)
  
### Polymorphic Relationships
- [One To One Polymorphic](#one-to-one-polymorphic)
- [One To Many-Polymorphic](#one-to-many-polymorphic)
- [Many To Many-Polymorphic](#many-to-many-polymorphic)
- [Custom Polymorphic Types](#custom-polymorphic-types)

### Querying Relations
- [Querying Relationship Existence](#querying-relationship-existence)
- [Querying Relationship Absence](#querying-relationship-absence)
- [Querying Polymorphic Relationships](#querying-polymorphic-relationships)
- [Aggregating Related Models](#aggregating-related-models)
- [Counting Related Models On Polymorphic Relationships](#counting-related-models-on-polymorphic-relationships)

### Eager Loading
- [Constraining Eager Loads](#constraining-eager-loads)
- [Lazy Eager Loading](#lazy-eager-loading)
### Inserting & Updating Related Models
-[The save Method](#the-save-method)
-[Recursively Saving Models & Relationships](#recursively-saving-models-&-relationships)
-[The create Method](#the-create-method)
-[Belongs To Relationships](#belongs-to-relationships)
    -Default Models](#default-models)
-[Many To Many Relationships](#many-to-many-relationships)
    -[Attaching / Detaching](#attaching-/-detaching)
	-[Syncing Associations](#syncing-associations)
	-[Toggling Associations](#toggling-associations)
	-[Saving Additional Data On A Pivot Table](#saving-additional-data-on-a-pivot-table)
	-[Updating A Record On A Pivot Table](#updating-a-record-on-a-pivot-table)

## One To One
![enter image description here](https://lh3.googleusercontent.com/JLHkNDXt8DOmmR9wnVobtD4x3SnbACaoJ7_-2C-2psLiq8ezkx-piQAyPPRUq-9DLKa5a4yPVZwNEvNKhQFPgJJFiAZel6v8_sCHRL3lGPLqoF8ikGP_8AS3pxFqFzWE1uaBV7hrMJmsSLLYwADDOD0BdF8je5IUiIVvOYSCTJQYrqctqaSd5h_6Vm-dqgfq1cA1IGyvYz4p07bMBb-vnSXeErfQEK3iG6olvagGQkzSSs0o110MYcFtOuhDqv0wQCuG0QtcFKVtQ7buvCQ8NeU0shm9bXk76ICoJdOVMCWVei0RWkWf7guyt0e20EgjH_2z1YtBE-IaOoK7N5KZZCSfeXQOha_Zckj-19Ie2c_7Kog7twRpGFO6d3xmzdNXcklzUxjKO2Np2MY2F_LHRNmwbEqTPY_ASgmS_U4uIz8qgIKBBg_Kx0eHX1gU-hukLKd62xbiAD3JGVUGC3Wnregcy8oLwWbhJwY100q2UuSsXs3Jb1oSJcVzhxR1oZlyQUBkzP7B-ayc7sEuAgjriIp1obSFqSkdlTdHLzbXCFVVDsBA9tOb_gR-H_yD-aUcoYuljOygCN8xfD2WYSqde03DR5PgCR7SbeHdqu0g5oTCCX5QJ9_mcJ2mT9bGZvWPoZqydhoVs6dfCBmfXExbhgdLGtNkC9j7Mn7ZaNe7I5kc1K8cJ0kwEvVAgnfT=w328-h270-no?authuser=0)


```php
class User extends Model
{
    /**
     * Get the phone record associated with the user.
     */
    public function phone()
    {
        return $this->hasOne('App\Models\Phone');
    }
}
```

```php
class Phone extends Model
{
    /**
     * Get the user that owns the phone.
     */
    public function user()
    {
        return $this->belongsTo('App\Models\User');
    }
}
```

```php
return $this->hasOne('App\Models\Phone', 'foreign_key', 'local_key');
```
`Accessing  from User to phone`
```php
$phone = User::find(1)->phone;
```

## One To Many
![enter image description here](https://lh3.googleusercontent.com/kvZSJWMkoePKyzx701ruNJWx-eEx_h6lIBXSSC11Y_kvd9ZLBx5JkXbjRYwrMuofWgI0-kS3RaXwvGs9iJoDd2wEozGb9sQqKxzdPxwQZbxbExIq6JCQCXQgF9PDRxnbTmtxTRcFyGirVcJ6FBXqJsnP_SVQLz9WbwpuCLZKL6WuHqTYLBV26p4EkmttVryeB2SRz5B89CytKuf74dNMgtGL2lGcVT5VRSUj97ceWTacUTJEDOPde0OTtcUvzYl4Wu-ZIg2jQLvE6UeTsqPnu7NQy0PwOsOlheI-GKyLTjeUs2q_NlwtgRuMujFjyO3pqv2_DOmHoAVGSi8g4IlzZNOCBuzXXYa-F52Zo29kavG-mWOY-CKKNecfAzXTMer21Q0aJkvkvC9u_bpWXkmGgj-EJCGaEHPb1eqOF1K7STeZE-gfxMQa0QHpdDbaWyw6aOI96Re-Ovp8HQBdE1v7Qn3i6Se3yvMAjh5DmXbJQ-phHY8xjo4wkKH9zu_ny-x59NDSEul9uHcVHaH1wgGOPzWGYbQb_fZf1TJ1tKjLGJEKQAnMjDNHhOMjZUZQfNd8u9I1QAsIiu911-MXFNykSlP6FCq8pxtOSUvppp2IjwX7_Pz0wiS49jiMY1s2S1vdkdgGhjP_0MUBD0E8bHoju6okqsPcre120tLF2SHdMKT8d1u_jozuYFYKSXPq=w1329-h903-no?authuser=0)
```php
class Post extends Model
{
    /**
     * Get the comments for the blog post.
     */
    public function comments()
    {
        return $this->hasMany('App\Models\Comment');
    }
}
```
```php
class Comment extends Model
{
    /**
     * Get the post that owns the comment.
     */
    public function post()
    {
        return $this->belongsTo('App\Models\Post');
    }
}
```
##### Accessing FROM post to comments
```php
$comments = App\Models\Post::find(1)->comments;

foreach ($comments as $comment) {
    //
}
```
```php
$comment = App\Models\Post::find(1)->comments()->where('title', 'foo')->first();
```

##### Accessing FROM comments to post
```php
$comment = App\Models\Comment::find(1);

echo $comment->post->title;
```

## Many To Many

bir mağazada birkaç farklı ürün olabilir ve bir ürün birkaç farklı mağazada olabilir
![enter image description here](https://lh3.googleusercontent.com/yO7Upx21Zz6Ej8hQhMYVx5S9nQqEanxwVz9JLwY3EtiLhFNQvUI44dnr6fqGJGSF9VvL765kC8VJnVSsvnYL8fHzhh2HOH2ed8ZMH1IA9HzVD59ze5x5udJ61aeuiCbXFOKRuQKTow7YZ5WsJ1h_o3kJvlBzaoL4-ydnqBiATnaKaqfW_mgZXToQBhzHtAhZ5f50vhbBTWOOaUgWUE6nj1OccQF2K6K2UGofVDc6H59kNfXl4_ZVtQtJBYFLNsqAJwATBvVG--lRTPDN4Hj9MLyl6DsRH1UxpiFGXz5acol7y5kCEXLK83Ufb-z5CP6UbJReACGL80G8bjxYqph3E3NjDuYTBXf7yQKjYVBkm0GAkcVOZirkhZuSSgLioD_-NJuDPRDIP2Iqp8m8pmzHtRRojJ4vXhTuv0hXtyyfdkSftJaQV1-mq1SZExZefC_rsSg64bc9Dj8VMNDA0ydZIsuad6ji9zKn3v4JwWbBp6cnT7Q0w9CDrd9FgBtd8QmLp-JpoxwJhV7Un6AqBndB_8-0ApDD2f6alm_o0JZYmkWLmL2LFb3Bd7UwJB1MfxfeNR432JSyb8fhz8zO31tg7zW0E88MOGt33-iJXolFJcjb-O7USdfepaAXlddKazpsefOdB9DuJrXpSghmb86oqFsmruX96RB8xDeL7toI9MDBbNgQDTBXXPZRaJWy=w1554-h903-no?authuser=0)
`table structure`

bir ürünün birkaç kategorisi olabilir ve bir katogori birkaç farklı üründe olabilir
![enter image description here](https://lh3.googleusercontent.com/nAlNYwq-XRReH5_bmSQXnLlV8z-6NwNzjVwYrNi0gbZqh_WkkQIiXww0p9jaj2lhRiMvO3ExJeRk0wQV6Gye66MYC7ujS5UbLmNh6j1lMXH9yy6F1PS7DsZyfbsl0hQqMG7TRXYy0ZhUoT-QzH5MhNP0Su7NR5tmuDeGJXLjmBRDAMQVOqWXPfSot0d95Au7r9AjRI2GW_6-IcCI_SsZ1L27yrZ9vo1IK3FlMrNl0N2I_Yde7WQ4riqgyF2FzPUeU60XjfA2A41cFAZHnRCMiKL6oS_nogkFzOt7aRn_YXg6E7DiLONxjoXW_qAUHPOoZZWCAFLfZ4iMe9EkYCxbuJIgp_8Gu3CS9iUrm5sBXe-lrKwqb1jjuloYgJoVvfs-BRKjOwKl8jp8NW6YvQprpmIH2qGl5DBxzz63c6txQSPMza7AMNC4XrTxQSw8YTlU-j3DRdSR-W5rxJAV8RpwIp_ktxQ7c2HHP9dg4BLKRv5-JJz0dCarAcDEPDqPmQyOR58T1dYpBcLFCCqpGAJ6sGQMVok8BvXg7DbM9MkTUeZ90yi_f1MywigiBF-F9VX7ImrHT4tw75bqsT2kAI2FdMDYPwMCRA9QesFINJuPMTDxj9oCho3nZ2WfD0pITj_hec-RQO45_5nZGwxH51QGvW6zZE6d8r63wDJs--oRqGVdc0yJT_2cFnN4F6s4=w1554-h903-no?authuser=0)

```php
users
    id - integer
    name - string

roles
    id - integer
    name - string

role_user
    user_id - integer
    role_id - integer
```
 `Model structure`
 ```php
class User extends Model
{
    /**
     * The roles that belong to the user.
     */
    public function roles()
    {
        return $this->belongsToMany('App\Models\Role');
    }
}
```
```php
class Role extends Model
{
    /**
     * The users that belong to the role.
     */
    public function users()
    {
        return $this->belongsToMany('App\Models\User');
    }
}
```
##### Accessing
```php
$roles = App\Models\User::find(1)->roles()->orderBy('name')->get();
```

### Retrieving Intermediate Table Columns
pivot table'daki attribute ulaşma

`model class`
```php
return $this->belongsToMany('App\Models\Role')->withPivot('column1', 'column2')->withTimestamps();
```
```php
$user = App\Models\User::find(1);

foreach ($user->roles as $role) {
    echo $role->pivot->created_at;
}
```
```php
$user = App\Models\User::find(1);

foreach ($user->roles as $role) {
    echo $role->pivot->col1;
}
```
### Customizing The pivot Attribute Name
```php
return $this->belongsToMany('App\Models\Podcast')
                ->as('subscription')
                ->withTimestamps();
```
```php
$users = User::with('podcasts')->get();

foreach ($users->flatMap->podcasts as $podcast) {
    echo $podcast->subscription->created_at;
}
```
### Filtering Relationships Via Intermediate Table Columns

`modelde`
```php
return $this->belongsToMany('App\Models\Role')->wherePivot('approved', 1);

return $this->belongsToMany('App\Models\Role')->wherePivotIn('priority', [1, 2]);

return $this->belongsToMany('App\Models\Role')->wherePivotNotIn('priority', [1, 2]);
```

### Defining Custom Intermediate Table Models
Many to many ve many to many polymorhpic yapılar için sadece kullanılabilir
`Role Model`
```php
class Role extends Model
{
    /**
     * The users that belong to the role.
     */
    public function users()
    {
        return $this->belongsToMany('App\Models\User')->using('App\Models\RoleUser');
    }
}
```
`Role User`
```php
class RoleUser extends Pivot
{
    //
}
```
You can combine `using` and `withPivot` in order to retrieve columns from the intermediate table. For example, you may retrieve the `created_by` and `updated_by` columns from the `RoleUser` pivot table by passing the column names to the `withPivot` method:
```php
class Role extends Model
{
    /**
     * The users that belong to the role.
     */
    public function users()
    {
        return $this->belongsToMany('App\Models\User')
                        ->using('App\Models\RoleUser')
                        ->withPivot([
                            'created_by',
                            'updated_by',
                        ]);
    }
}
```

##### Custom Pivot Models And Incrementing IDs

If you have defined a many-to-many relationship that uses a custom pivot model, and that pivot model has an auto-incrementing primary key, you should ensure your custom pivot model class defines an `incrementing` property that is set to `true`.

```php
/**
 * Indicates if the IDs are auto-incrementing.
 */
public $incrementing = true;
```

## Has One Through

```php
mechanics
    id - integer
    name - string

cars
    id - integer
    model - string
    mechanic_id - integer

owners
    id - integer
    name - string
    car_id - integer
```
```php

<?php
class Mechanic extends Model
{
    /**
     * Get the car's owner.
     */
    public function carOwner()
    {
        return $this->hasOneThrough('App\Models\Owner', 'App\Models\Car');
    }
}
```

```php
class Mechanic extends Model
{
    /**
     * Get the car's owner.
     */
    public function carOwner()
    {
        return $this->hasOneThrough(
            'App\Models\Owner',
            'App\Models\Car',
            'mechanic_id', // Foreign key on cars table...
            'car_id', // Foreign key on owners table...
            'id', // Local key on mechanics table...
            'id' // Local key on cars table...
        );
    }
}
```
## Has Many Through
https://www.youtube.com/watch?v=O5JGGvYTb4E

```php
countries
    id - integer
    name - string

users
    id - integer
    country_id - integer
    name - string

posts
    id - integer
    user_id - integer
    title - string
```
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Country extends Model
{
    /**
     * Get all of the posts for the country.
     */
    public function posts()
    {
        return $this->hasManyThrough('App\Models\Post', 'App\Models\User');
    }
}
```

```php
class Country extends Model
{
    public function posts()
    {
        return $this->hasManyThrough(
            'App\Models\Post',
            'App\Models\User',
            'country_id', // Foreign key on users table...
            'user_id', // Foreign key on posts table...
            'id', // Local key on countries table...
            'id' // Local key on users table...
        );
    }
}
```

## Polymorphic Relationships
### One To One Polymorphic
```php
posts
    id - integer
    name - string

users
    id - integer
    name - string

images
    id - integer
    url - string
    imageable_id - integer
    imageable_type - string
```
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Image extends Model
{
    /**
     * Get the owning imageable model.
     */
    public function imageable()
    {
        return $this->morphTo();
    }
}

class Post extends Model
{
    /**
     * Get the post's image.
     */
    public function image()
    {
        return $this->morphOne('App\Models\Image', 'imageable');
    }
}

class User extends Model
{
    /**
     * Get the user's image.
     */
    public function image()
    {
        return $this->morphOne('App\Models\Image', 'imageable');
    }
}
```
##### Retrieving The Relationship
```php
$post = App\Models\Post::find(1);
$image = $post->image;
```
```php
$post = App\Models\Post::find(1);

$image = $post->image;
```
### One To Many Polymorphic
[https://www.itsolutionstuff.com/post/laravel-one-to-many-polymorphic-relationship-tutorialexample.html](https://www.itsolutionstuff.com/post/laravel-one-to-many-polymorphic-relationship-tutorialexample.html)
Videonun bir çok yorumu olabilir
Postun bir çok yorumu olabilir
burada yorumlar tablosu ortak

![enter image description here](https://lh3.googleusercontent.com/v1S-hLuDqE-oVFWBmiWlvttD5Sukb-KkYG_AD5HirM3IjyY8xihNVKzuaBx3Ep0O81GwEIK_AiM_XKA5Ad4M-_iA4UUURdGiP4wWD9Iq6w0H6kLVnIlquiBZBGvYAWOR-QvKpDvK65M6vjJtstbsh8u3lodvCw8FzwPx3GTi9Ca7okSSMMsVImxlnx2FamgyBFHKgNoIqp3JCcsikdWYqq0AA4BvKbE85PYjJgLD9HABEp1vBWy6b2OBcTxKljeDrmwWFNNFSwA1_u1b14jEyKcQQ2IM5idVtU6Z4gWtkTzpzF2EWtqIvkniqikvNW2Nqou6GccZtmBXL77x1MOWhikZ_eBvxp8B02WwmWKLOsn9sndq5VMpTyV1PNoWtY8HoujZOwLRPyikKVfGMUt1sFX__Uu2jq6CzF6OvHlv13WjpNAGCXy2dSkwC_OqyAtYxx6FtkxVg1eMOqLrESu7z6J_iXJgwRUMfauLvJwMyFA2QKJpEz57iAYUX2De2TFAzISOBXdvfnDtTP7L8golG7qhpSM-Zg_VvhaAlUYCVp-c8o4cyAACaTWDVQP8FwYiXuIornpmnmjRC27OJdNd8kcalXu5XNanjqXqEguBwseibctai3kKDyqBKeJWdm4qNMThlSkemvFfigY9sxV5x85j4C12_2N9yxzf1kGQ0--xjnTplpMINQKm05Vp=w875-h399-no?authuser=0)


![enter image description here](https://lh3.googleusercontent.com/rF3auciaOLapfTFjhgAhDjnJu2LLRrggOGgRHOBMWhAek48BUEfUm9atN84mqXWeoGsbQmm-22IdXYRRSsEtsDuq8onrTSzr7TyOez_irCeg09XcZ86osYAiGQ2HycKxQJZP4rsQbarkaKw6S_OFmqFuFWdT7uB_OyP5Ysn9mqdwGMMoS8ur9Wo3gUf6Zdo14WmD9uL9VVB74NhkEp22_UCKUNtYEY88Vhn6zXbWQJPYHGXeR7QJz1Dj6HYyUxUwThPh4_wNxGNIroBhgedMQ0dlPsfQPUZD6YvKaju1SrBLHu3fbzMEOvoyNm6ZFuMQR4kUgwAelCmqt-a6oKzmDZg4ltIAbg-aqWkiTemcPjy4k2RlwlvaqRUaoG75bMaJ16KvrJwFP-QIEsQFIsTjOz86g9c9OAhOjgn1Biq6xyMvSzdLmXzgKWFMWnisLhIq0sXlGIusPQsPCqZcuvHs8lcR8BhJr5N8F5tmy7bfWqQVhsnEbHQ4JOMuV_oDeWczdQNpB_Nn0wVrCho2ttt79iWROtA0ngbyPZ3MfzJwz41z02YIDgK0R0jX-91HTvdZpdZciU225JU2FEpLrffgN6ujj4VywY0WBtcrB6JNzrNcibZ6ckuMNP-1wYLqA-EtEUxDwiH3xv_Gj4rgpPouVSzIIvl9r_Ohq0ZN-0ZxA6G1RigEbSZ0tR4pzhqg=w875-h182-no?authuser=0)


![enter image description here](https://lh3.googleusercontent.com/rXVb2H5RxEXa4YM_RpNIW6OEXxN8a9rC-fT21E4oDQyZL7E03t3I-EtxFvdGmDPdy17QTLrZaLov2onBFJwPYVGPEv3X4xVyZHPa8yiKZ6LEb6eBd3fOYpBpwVehMR6vmg-qY7boP8RzNVqrGCZ8aROYykpzHDv3BZjv5DQiSpmF8QmnFC_ULKqeJ1ioP4ygqYRbJLUHSblIxRJh51Vs28Dn4tL7a5mMbKCFGDX5mU6eEkIlWH4MdZZ-SfD0gFkPFYg2OZiwAi910KK5Jauc5vbDHXaUbA6lSz2IGMNxeZ-52rn8gE7MstTyDt9H4JgKGumwPKGGSwpCKVaKzh2ggOB8O0_uNG7EPc51S5KLXOtrF1xK1Ev8nWZTf3Q5K8Yurk3OUlP9GQ_ddouGKTDIdWNk9LpGumK43ma3lJx9KuCDV2Mv7PpckEJjXmysypNmUDCOi0_mYKRtgdlt747TCERfy8mVzPJtUAz5zefPW0SF2DAf-oj54H-Cev-7yNHUOT_F3-_1Qh2NH1aFeG9Zj3oW9dHQ3O2nnUfSvJNhoiw0PwgSZ2tY0_ROVWGHUHiJggSYqmbIMCHbmzbgE-xtIyss6Usa_OkswqFSgv7MKhYW-i94p48h0DBXROpEYyhO15U2tdJXzjM02PgW7a-xLrUTVbnWHYcvgs2Nm4fW4sK66Dz7DE_r33Di9lop=w1188-h833-no?authuser=0)

```php
posts
    id - integer
    title - string
    body - text

videos
    id - integer
    title - string
    url - string

comments
    id - integer
    body - text
    commentable_id - integer
    commentable_type - string
```
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Comment extends Model
{
    /**
     * Get the owning commentable model.
     */
    public function commentable()
    {
        return $this->morphTo();
    }
}

class Post extends Model
{
    /**
     * Get all of the post's comments.
     */
    public function comments()
    {
        return $this->morphMany('App\Models\Comment', 'commentable');
    }
}

class Video extends Model
{
    /**
     * Get all of the video's comments.
     */
    public function comments()
    {
        return $this->morphMany('App\Models\Comment', 'commentable');
    }
}
```
##### Retrieving The Relationship
```php
$post = App\Models\Post::find(1);

foreach ($post->comments as $comment) {
    //
}
```
```php
$comment = App\Models\Comment::find(1);

$commentable = $comment->commentable;
```
### Many To Many Polymorphic
```php
posts
    id - integer
    name - string

videos
    id - integer
    name - string

tags
    id - integer
    name - string

taggables
    tag_id - integer
    taggable_id - integer
    taggable_type - string
```

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    /**
     * Get all of the tags for the post.
     */
    public function tags()
    {
        return $this->morphToMany('App\Models\Tag', 'taggable');
    }
}
```
```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Tag extends Model
{
    /**
     * Get all of the posts that are assigned this tag.
     */
    public function posts()
    {
        return $this->morphedByMany('App\Models\Post', 'taggable');
    }

    /**
     * Get all of the videos that are assigned this tag.
     */
    public function videos()
    {
        return $this->morphedByMany('App\Models\Video', 'taggable');
    }
}
```

##### Retrieving The Relationship
```php
$post = App\Models\Post::find(1);

foreach ($post->tags as $tag) {
    //
}
```


### Custom Polymorphic Types
```php
Relation::morphMap([
    'posts' => 'App\Models\Post',
    'videos' => 'App\Models\Video',
]);
```

## Querying Relations
### Querying Relationship Existence
. For example, imagine you want to retrieve all blog posts that have at least one comment. To do so, you may pass the name of the relationship to the `has` and `orHas` methods:
```php
// Retrieve all posts that have at least one comment...
$posts = App\Models\Post::has('comments')->get();
```
You may also specify an operator and count to further customize the query:
```php
// Retrieve all posts that have three or more comments...
$posts = App\Models\Post::has('comments', '>=', 3)->get();
```
Nested  `has`  statements may also be constructed using "dot" notation. For example, you may retrieve all posts that have at least one comment and vote:
```php
// Retrieve posts that have at least one comment with votes...
$posts = App\Models\Post::has('comments.votes')->get();
```
If you need even more power, you may use the `whereHas` and `orWhereHas` methods to put "where" conditions on your `has` queries. These methods allow you to add customized constraints to a relationship constraint, such as checking the content of a comment:
```php
use Illuminate\Database\Eloquent\Builder;

// Retrieve posts with at least one comment containing words like foo%...
$posts = App\Models\Post::whereHas('comments', function (Builder $query) {
    $query->where('content', 'like', 'foo%');
})->get();

// Retrieve posts with at least ten comments containing words like foo%...
$posts = App\Models\Post::whereHas('comments', function (Builder $query) {
    $query->where('content', 'like', 'foo%');
}, '>=', 10)->get();
```
### Querying Relationship Absence
```php
$posts = App\Models\Post::doesntHave('comments')->get();
```
For example, imagine you want to retrieve all blog posts that **don't** have any comments. To do so, you may pass the name of the relationship to the `doesntHave` and `orDoesntHave` methods:

```php
$posts = App\Models\Post::doesntHave('comments')->get();
```
If you need even more power, you may use the  `whereDoesntHave`  and  `orWhereDoesntHave`  methods to put "where" conditions on your  `doesntHave`  queries. These methods allow you to add customized constraints to a relationship constraint, such as checking the content of a comment:
```php
use Illuminate\Database\Eloquent\Builder;
$posts = App\Models\Post::whereDoesntHave('comments', function (Builder $query) {
    $query->where('content', 'like', 'foo%');
})->get();
```

### Aggregating Related Models
If you want to count the number of results from a relationship without actually loading them you may use the `withCount` method, which will place a `{relation}_count` column on your resulting models. For example:
```php
$posts = App\Models\Post::withCount('comments')->get();
foreach ($posts as $post) {
    echo $post->comments_count;
}
```
You may add the "counts" for multiple relations as well as add constraints to the queries:
```php
use Illuminate\Database\Eloquent\Builder;

$posts = App\Models\Post::withCount(['votes', 'comments' => function (Builder $query) {
    $query->where('content', 'like', 'foo%');
}])->get();

echo $posts[0]->votes_count;
echo $posts[0]->comments_count;
```
You may also alias the relationship count result, allowing multiple counts on the same relationship:
```php
$posts = App\Models\Post::withCount([
    'comments',
    'comments as pending_comments_count' => function (Builder $query) {
        $query->where('approved', false);
    },
])->get();

echo $posts[0]->comments_count;
echo $posts[0]->pending_comments_count;
```

If you're combining `withCount` with a `select` statement, ensure that you call `withCount` after the `select` method:

```php
$posts = App\Models\Post::select(['title', 'body'])->withCount('comments')->get();

echo $posts[0]->title;
echo $posts[0]->body;
echo $posts[0]->comments_count;
```
In addition, using the  `loadCount`  method, you may load a relationship count after the parent model has already been retrieved:
```php
$book = App\Models\Book::first();

$book->loadCount('genres');
```
If you need to set additional query constraints on the eager loading query, you may pass an array keyed by the relationships you wish to load. The array values should be `Closure` instances which receive the query builder instance:
```php
$book->loadCount(['reviews' => function ($query) {
    $query->where('rating', 5);
}])
```
##### Other Aggregate Functions
In addition to the `withCount` method, Eloquent provides `withMin`, `withMax`, `withAvg`, and `withSum`. These methods will place a `{relation}_{function}_{column}` column on your resulting models. For example:
```php
$posts = App\Models\Post::withSum('comments', 'votes')->get();

foreach ($posts as $post) {
    echo $post->comments_sum_votes;
}
```
These additional aggregate operations may also be performed on Eloquent models that have already been retrieved:
```php
$post = App\Models\Post::first();

$post->loadSum('comments', 'votes');
```
### Counting Related Models On Polymorphic Relationships
In this example, let's assume  `Photo`  and  `Post`  models may create  `ActivityFeed`  models. Additionally, let's assume that  `Photo`  models are associated with  `Tag`  models, and  `Post`  models are associated with  `Comment`  models.

Using these model definitions and relationships, we may retrieve  `ActivityFeed`  model instances and eager load all  `parentable`  models and their respective nested relationship counts:
```php
use Illuminate\Database\Eloquent\Relations\MorphTo;

$activities = ActivityFeed::query()
    ->with(['parentable' => function (MorphTo $morphTo) {
        $morphTo->morphWithCount([
            Photo::class => ['tags'],
            Post::class => ['comments'],
        ]);
    }])->get();
```
In addition, you may use the `loadMorphCount` method to eager load all nested relationship counts on the various entities of the polymorphic relation if the `ActivityFeed` models have already been retrieved:
```php
$activities = ActivityFeed::with('parentable')
    ->get()
    ->loadMorphCount('parentable', [
        Photo::class => ['tags'],
        Post::class => ['comments'],
    ]);
```
## Eager Loading
```php
class Book extends Model
{
   // Get the author that wrote the book.
    public function author()
    {
        return $this->belongsTo('App\Models\Author');
    }
}
```
```php
$books = App\Models\Book::with('author')->get();

foreach ($books as $book) {
    echo $book->author->name;
}
```
For this operation, only two queries will be executed:

```php
select * from books

select * from authors where id in (1, 2, 3, 4, 5, ...)
```
##### Eager Loading Multiple Relationships
```php
$books = App\Models\Book::with(['author', 'publisher'])->get();
```
##### Nested Eager Loading
```php
$books = App\Models\Book::with('author.contacts')->get();
```
##### Nested Eager Loading morphTo Relationships
```php
class ActivityFeed extends Model
{
    /**
     * Get the parent of the activity feed record.
     */
    public function parentable()
    {
        return $this->morphTo();
    }
}
```
In this example, let's assume  `Event`,  `Photo`, and  `Post`  models may create  `ActivityFeed`  models. Additionally, let's assume that  `Event`  models belong to a  `Calendar`  model,  `Photo`  models are associated with  `Tag`  models, and  `Post`  models belong to an  `Author`  model.

Using these model definitions and relationships, we may retrieve  `ActivityFeed`  model instances and eager load all  `parentable`  models and their respective nested relationships:

```php
use Illuminate\Database\Eloquent\Relations\MorphTo;

$activities = ActivityFeed::query()
    ->with(['parentable' => function (MorphTo $morphTo) {
        $morphTo->morphWith([
            Event::class => ['calendar'],
            Photo::class => ['tags'],
            Post::class => ['author'],
        ]);
    }])->get();
```
##### Eager Loading Specific Columns
```php
$books = App\Models\Book::with('author:id,name')->get();
```
##### Eager Loading By Default
Sometimes you might want to always load some relationships when retrieving a model. To accomplish this, you may define a `$with` property on the model:
```php
class Book extends Model
{
    /**
     * The relationships that should always be loaded.
     * @var array
     */
    protected $with = ['author'];

    /**
     * Get the author that wrote the book.
     */
    public function author()
    {
        return $this->belongsTo('App\Models\Author');
    }
}
```
If you would like to remove an item from the  `$with`  property for a single query, you may use the  `without`  method:

```php
$books = App\Models\Book::without('author')->get();
```

###  Constraining Eager Loads
```php
$users = App\Models\User::with(['posts' => function ($query) {
    $query->where('title', 'like', '%first%');
}])->get();
```
```php
$users = App\Models\User::with(['posts' => function ($query) {
    $query->orderBy('created_at', 'desc');
}])->get();
```
### Constraining Eager Loading Of MorphTo Relationships
In this example, Eloquent will only eager load posts that have not been hidden and videos have a `type` value of "educational".

```php
$comments = Comment::with(['commentable' => function (MorphTo $morphTo) {
    $morphTo->constrain([
        Post::class => function (Builder $query) {
            $query->whereNull('hidden_at');
        },
        Video::class => function (Builder $query) {
            $query->where('type', 'educational');
        },
    ]);
}])->get();
```
### Lazy Eager Loading
Sometimes you may need to eager load a relationship after the parent model has already been retrieved. For example, this may be useful if you need to dynamically decide whether to load related models:

```php
$books = App\Models\Book::all();

if ($someCondition) {
    $books->load('author', 'publisher');
}
```
If you need to set additional query constraints on the eager loading query, you may pass an array keyed by the relationships you wish to load. The array values should be `Closure` instances which receive the query instance
```php
$author->load(['books' => function ($query) {
    $query->orderBy('published_date', 'asc');
}]);
```
To load a relationship only when it has not already been loaded, use the  `loadMissing`  method:

```php
public function format(Book $book)
{
    $book->loadMissing('author');

    return [
        'name' => $book->name,
        'author' => $book->author->name,
    ];
}
```
##### Nested Lazy Eager Loading & morphTo
```php
class ActivityFeed extends Model
{
    /**
     * Get the parent of the activity feed record.
     */
    public function parentable()
    {
        return $this->morphTo();
    }
}
```
In this example, let's assume  `Event`,  `Photo`, and  `Post`  models may create  `ActivityFeed`  models. Additionally, let's assume that  `Event`  models belong to a  `Calendar`  model,  `Photo`  models are associated with  `Tag`  models, and  `Post`  models belong to an  `Author`  model.

Using these model definitions and relationships, we may retrieve  `ActivityFeed`  model instances and eager load all  `parentable`  models and their respective nested relationships:
```php
$activities = ActivityFeed::with('parentable')
    ->get()
    ->loadMorph('parentable', [
        Event::class => ['calendar'],
        Photo::class => ['tags'],
        Post::class => ['author'],
    ]);
```
## Inserting & Updating Related Models
### The Save Method
```php
$comment = new App\Models\Comment(['message' => 'A new comment.']);
$post = App\Models\Post::find(1);
$post->comments()->save($comment);
```
```php
$post = App\Models\Post::find(1);
$post->comments()->saveMany([
    new App\Models\Comment(['message' => 'A new comment.']),
    new App\Models\Comment(['message' => 'Another comment.']),
]);
```
The `save` and `saveMany` methods will not add the new models to any in-memory relationships that are already loaded onto the parent model. If you plan on accessing the relationship after using the `save` or `saveMany` methods, you may wish to use the `refresh` method to reload the model and its relationships:
```php
$post->comments()->save($comment);
$post->refresh();
// All comments, including the newly saved comment...
$post->comments;
```
##### Recursively Saving Models & Relationships
If you would like to  `save`  your model and all of its associated relationships, you may use the  `push`  method:

```php
$post = App\Models\Post::find(1);

$post->comments[0]->message = 'Message';
$post->comments[0]->author->name = 'Author Name';

$post->push();
```
### The Create Method
```php
$post = App\Models\Post::find(1);
$comment = $post->comments()->create([
    'message' => 'A new comment.',
]);
```
In addition to the  `save`  and  `saveMany`  methods, you may also use the  `create`  method, which accepts an array of attributes, creates a model, and inserts it into the database. Again, the difference between  `save`  and  `create`  is that  `save`  accepts a full Eloquent model instance while  `create`  accepts a plain PHP  `array`:
```php
$post = App\Models\Post::find(1);
$comment = $post->comments()->create([
    'message' => 'A new comment.',
]);
```
```php
$post = App\Models\Post::find(1);
$post->comments()->createMany([
    [
        'message' => 'A new comment.',
    ],
    [
        'message' => 'Another new comment.',
    ],
]);
```
You may also use the `findOrNew`, `firstOrNew`, `firstOrCreate` and `updateOrCreate` methods to [create and update models on relationships](https://laravel.com/docs/8.x/eloquent#other-creation-methods).

### Belongs To Relationships
When updating a belongsTo relationship, you may use the associate method. This method will set the foreign key on the child model:
```php
$account = App\Models\Account::find(10);
$user->account()->associate($account);
$user->save();
```
When removing a  `belongsTo`  relationship, you may use the  `dissociate`  method. This method will set the relationship's foreign key to  `null`:

```php
$user->account()->dissociate();

$user->save();
```
##### Default Models
The  `belongsTo`,  `hasOne`,  `hasOneThrough`, and  `morphOne`  relationships allow you to define a default model that will be returned if the given relationship is  `null`. This pattern is often referred to as the  [Null Object pattern](https://en.wikipedia.org/wiki/Null_Object_pattern)  and can help remove conditional checks in your code. In the following example, the  `user`  relation will return an empty  `App\Models\User`  model if no  `user`  is attached to the post:

```php
/**
 * Get the author of the post.
 */
public function user()
{
    return $this->belongsTo('App\Models\User')->withDefault();
}
```

To populate the default model with attributes, you may pass an array or Closure to the  `withDefault`  method:

```php
/**
 * Get the author of the post.
 */
public function user()
{
    return $this->belongsTo('App\Models\User')->withDefault([
        'name' => 'Guest Author',
    ]);
}

/**
 * Get the author of the post.
 */
public function user()
{
    return $this->belongsTo('App\Models\User')->withDefault(function ($user, $post) {
        $user->name = 'Guest Author';
    });
}
```

## Many To Many Relationships
### Attaching / Detaching

Eloquent also provides a few additional helper methods to make working with related models more convenient. For example, let's imagine a user can have many roles and a role can have many users. To attach a role to a user by inserting a record in the intermediate table that joins the models, use the  `attach`  method:

```php
$user = App\Models\User::find(1);

$user->roles()->attach($roleId);
```

When attaching a relationship to a model, you may also pass an array of additional data to be inserted into the intermediate table:

```php
$user->roles()->attach($roleId, ['expires' => $expires]);
```

Sometimes it may be necessary to remove a role from a user. To remove a many-to-many relationship record, use the  `detach`  method. The  `detach`  method will delete the appropriate record out of the intermediate table; however, both models will remain in the database:

```php
// Detach a single role from the user...
$user->roles()->detach($roleId);

// Detach all roles from the user...
$user->roles()->detach();
```

For convenience,  `attach`  and  `detach`  also accept arrays of IDs as input:

```php
$user = App\Models\User::find(1);

$user->roles()->detach([1, 2, 3]);

$user->roles()->attach([
    1 => ['expires' => $expires],
    2 => ['expires' => $expires],
]);
```

### Syncing Associations

You may also use the  `sync`  method to construct many-to-many associations. The  `sync`  method accepts an array of IDs to place on the intermediate table. Any IDs that are not in the given array will be removed from the intermediate table. So, after this operation is complete, only the IDs in the given array will exist in the intermediate table:

```php
$user->roles()->sync([1, 2, 3]);
```

You may also pass additional intermediate table values with the IDs:

```php
$user->roles()->sync([1 => ['expires' => true], 2, 3]);
```

If you do not want to detach existing IDs, you may use the  `syncWithoutDetaching`  method:

```php
$user->roles()->syncWithoutDetaching([1, 2, 3]);
```

### Toggling Associations

The many-to-many relationship also provides a  `toggle`  method which "toggles" the attachment status of the given IDs. If the given ID is currently attached, it will be detached. Likewise, if it is currently detached, it will be attached:

```php
$user->roles()->toggle([1, 2, 3]);
```

### Saving Additional Data On A Pivot Table

When working with a many-to-many relationship, the  `save`  method accepts an array of additional intermediate table attributes as its second argument:

```php
App\Models\User::find(1)->roles()->save($role, ['expires' => $expires]);
```

### Updating A Record On A Pivot Table

If you need to update an existing row in your pivot table, you may use  `updateExistingPivot`  method. This method accepts the pivot record foreign key and an array of attributes to update:

```php
$user = App\Models\User::find(1);

$user->roles()->updateExistingPivot($roleId, $attributes);
```




# Class Curriculum - laraveldaily (26 Dec 2018)

## Eloquent Model Options and Settings
 - [Artisan Command make:model with (hidden) options](#artisan-command-makemodel-with-hidden-options)
 - [Singular or Plural? What about multiple words?](#singular-or-plural-what-about-multiple-words)
 - [Saving a Model: $fillable or $guarded?](#saving-a-model-fillable-or-guarded)
 - [Properties for Tables, Keys, Increments, Pages and Dates](#properties-for-tables-keys-increments-pages-and-dates)

## Create/Update in Eloquent
 -  ["Magic" methods: FirstOrCreate() and other 2-in-1s](#magic-methods-firstorcreate-and-other-2-in-1s)
 -  [Model Observers: "listening" to record changes](#model-observers-listening-to-record-changes)
 -  [Accessors and Mutators: Change Model Values](#accessors-and-mutators-change-model-values)
 -  [Database Seeds and Factories: Prepare Dummy Data](#database-seeds-and-factories-prepare-dummy-data)
 -  [Seeds and Factories with Relationships](#seeds-and-factories-with-relationships)
 -  [Check Methods/Properties in Eloquent API Docs](#check-methodsproperties-in-eloquent-api-docs)


## Querying and Filtering Data Effectively
 -  [Advanced find() and all(): Methods and Parameters](#advanced-find-and-all-methods-and-parameters)
 -  [WhereX Magic Methods for Fields and Dates](#wherex-magic-methods-for-fields-and-dates)
 -  [Brackets to Eloquent: (A and B) or (C and D)](#brackets-to-eloquent-a-and-b-or-c-and-d)
 -  [Query Scopes: Where Conditions Applied Globally](#query-scopes-where-conditions-applied-globally)
 -  [Eloquent when(): More Elegant if-statement](#eloquent-when-more-elegant-if-statement)
 -  [Ordering by Relationship: orderBy vs sortBy](#ordering-by-relationship-orderby-vs-sortby)
 -  [Raw Database Queries with Examples](#raw-database-queries-with-examples)


## Eloquent Collections and their Methods
 - [Why You Need Collections and How to Use Them](#why-you-need-collections-and-how-to-use-them)
 - [Methods for Fetching and Transforming](#methods-for-fetching-and-transforming)
 - [Methods for Filtering with Callbacks](#methods-for-filtering-with-callbacks)
 - [Methods for Math Calculations](#methods-for-math-calculations)
 - [Methods for Debugging](#methods-for-debugging)
|

## Advanced Eloquent Relationships
 - [Polymorphic Relations Explained](#polymorphic-relations-explained)
 - [Polymorphic Many-to-Many Relations](#polymorphic-many-to-many-relations)
 - [Advanced Pivot Tables in Many-to-Many](#advanced-pivot-tables-in-many-to-many)
 - [HasManyThrough Relations](#hasmanythrough-relations)
 - [Creating Records with Relationships](#creating-records-with-relationships)
 - [Querying Records with Relationships](#querying-records-with-relationships)


## Eloquent Performance
 - [Laravel Debugbar: How to Measure Performance](#laravel-debugbar-how-to-measure-performance)
 - [Performance Test: Eloquent vs Query Builder vs SQL](#performance-test-eloquent-vs-query-builder-vs-sql)
 - [N+1 Problem and Eager Loading: Be Careful with Eloquent](#n1-problem-and-eager-loading-be-careful-with-eloquent)
 - [Caching in Eloquent](#caching-in-eloquent)


## Useful Packages to Extend Eloquent
 - [spatie/laravel-medialibrary: Associate files with Eloquent models](#spatielaravel-medialibrary-associate-files-with-eloquent-models)
 - [dimsav/laravel-translatable: Package for Multilingual Models](#dimsavlaravel-translatable-package-for-multilingual-models)
 - [spatie/eloquent-sortable: Sortable Eloquent Models](https://github.com/spatie/eloquent-sortable)
 - [spatie/laravel-tags: Add Tags and Taggable Behavior](https://github.com/spatie/laravel-tags)
 - [owen-it/laravel-auditing: Record the Changes From Models](https://github.com/owen-it/laravel-auditing)
 - [michaeldyrynda/laravel-cascade-soft-deletes: Cascade Delete & Restore](https://github.com/michaeldyrynda/laravel-cascade-soft-deletes)

# Eloquent Model Options and Settings

## Artisan Command make:model with (hidden) options 

 Create a model instance:
 
    php artisan make:model Post

 Create a model instance with migration:

    php artisan make:model Post --migration
    php artisan make:model Post -m

 Create a model instance with migration and controller:

     php artisan make:model Post -mc

 Create a model instance with migration and resource controller:

     php artisan make:model Post -mcr

 Create a model instance with migration,resource controller and factory:

    php artisan make:model Post -mcrf

Shorcut to create a model instance with migration,resource controller and factory:

    php artisan make:model Post -a

Display and describe the command's available arguments and options:

    php artisan make:model --help


## Singular or Plural? What about multiple words?

What | How | Good | Bad
------------ | ------------- | ------------- | -------------
Controller | singular | ArticleController | ~~ArticlesController~~
Model | singular | User | ~~Users~~
Table | plural | article_comments | ~~article_comment, articleComments~~
Migration | - | 2017_01_01_000000_create_articles_table | ~~2017_01_01_000000_articles~~

Read more naming conventions [Laravel best practices](https://github.com/alexeymezenin/laravel-best-practices/blob/master/README.md#follow-laravel-naming-conventions)


## Saving a Model: $fillable or $guarded? 

Mass assignment: means to send an array to the model to directly create a new record in Database.

$fillable specifies which attributes in the table should be mass-assignable.

    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Article extends Model
    {
        /**
        * The attributes that are mass assignable.
        *
        * @var array
        */
        protected $fillable = ['title', 'article_text'];
    }

$guarded specifies which attributes in the table shouldn't be mass-assignable.
    
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Article extends Model
    {
        /**
        * The attributes that are mass assignable.
        *
        * @var array
        */
        protected $guarded = ['id'];
    }

## Properties for Tables, Keys, Increments, Pages and Dates 

`$table` specifies a custom table.

`$primaryKey` specifies a custom primary key. 

`$incrementing` specifies a non-incrementing or a non-numeric primary key.

`$perPage` specifies the number of items per page in paginate.

`$timestamps` disable created_at and updated_at columns.

`CREATED_AT` and `UPDATED_AT` specify the custom names of the columns used to store the timestamps.

`$dateFormat` specifies the custom format of your timestamps.

`$dates` converts columns to instances of Carbon.

    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Article extends Model
    {
        /**
        * The attributes that are mass assignable.
        *
        * @var array
        */
        protected $table = 'user_articles';

        protected $primaryKey = 'article_id';

        public $incrementing = false;

        $perPage = 5;

        public $timestamps = false;

        const CREATED_AT = 'creation_date';

        const UPDATED_AT = 'last_update';

        protected $dateFormat = 'm/d/Y H:i:s';

        protected $dates = [
            'created_at',
            'updated_at',
            'deleted_at'
        ];
                
    }

# Create/Update in Eloquent

## "Magic" methods: FirstOrCreate() and other 2-in-1s

There are two other methods you may use to create models by mass assigning attributes:  firstOrCreate and firstOrNew. The firstOrCreate method will attempt to locate a database record using the given column / value pairs. If the model can not be found in the database, a record will be inserted with the attributes from the first parameter, along with those in the optional second parameter. [Laravel docs](https://laravel.com/docs/5.7/eloquent#other-creation-methods)

    function store(Request $request)
    {
        $article = Article::where('title', $request->title)->first();
        if(!$article){
            $article = Article::create([
                'title' => $request->title,
                'article_text' => $request->article_text
            ]);
        }

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

It can be replaced by:

    function store(Request $request)
    {
        $article = Article::firstOrCreate(['title' => $request->title], ['article_text' => $request->article_text]);

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

    function store(Request $request)
    {
        $article = Article::firstOrNew(['title' => $request->title], ['article_text' => $request->article_text]);
        $article->field = $value;
        $article->save();

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

`updateOrCreate` updates an existing model or create a new model if none exists.

    function store(Request $request)
    {
        $article = Article::where('title', $request->title)->where('user_id', auth()->id()->first();
        if($article){
            $article->update(['article_text' => $request-article_text]);
        }else{
            $article = Article::create([
                'title' => $request->title,
                'article_text' => $request->article_text.
                'user_id' => auth()->id
            ]);
        }

        $article = Article::updateOrCreate(['title' => $request->title, 'user_id' => auth()->id()]);

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

It can be replaced by:

        function store(Request $request)
    {
        $article = Article::updateOrCreate(['title' => $request->title, 'user_id' => auth()->id()],
        ['article_text' => $request->article_text]);

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

## Model Observers: "listening" to record changes 

Observers are used to group event listeners for a model, for create a new observer run:

    php artisan make:observer ArticleObserver --model=Article

Register the observer in the `AppServiceProvider`:

    <?php

    namespace App\Providers;

    use App\Article;
    use App\Observers\UserObserver;
    use Illuminate\Support\ServiceProvider;

    class AppServiceProvider extends ServiceProvider
    {
        /**
        * Bootstrap any application services.
        *
        * @return void
        */
        public function boot()
        {
            Article::observe(ArticleObserver::class);
        }

        /**
        * Register the service provider.
        *
        * @return void
        */
        public function register()
        {
            //
        }
    }

Article model:

    public function store(Request $request)
    {
        Article::create($request->all());
        return redirect()->route('articles.index');
    }

ArticleObserver:

    public function createdArticle(Article $article)
    {
        info('Article is saved');
    }

Every time an article is created, you will have a message in log.

    [2018-09-19 20:15:26] local.INFO: Article is saved

## Accessors and Mutators: Change Model Values 

Accessors and mutators allow you to format Eloquent attribute values when you retrieve or set them on model instances. 

Accesor -> get Attribute
Mutator -> set Attribute

Create a `getFullNameAttribute` method on model:

    public function getFullNameAttribute()
    {
        return $this->name . ' ' . $this->surname;
    }

To access the value of the accessor, you may access the  `first_name` attribute on a model instance:

    <td>{{ $user->full_name }}</td>


    public function setNameAttribute($value)
    {
        $this->attributes['name'] = ucfirst($value);
    }

to set the first_name attribute to Taylor:

    $user->first_name = 'taylor';

## Database Seeds and Factories: Prepare Dummy Data

### Seeders

Seeding your database with test data using seed classes. Create seeder run:

    php artisan make:seeder UsersTableSeeder

add a database insert statement to the run method:

    <?php

    use Illuminate\Database\Seeder;

    class UserTableSeeder extends Seeder
    {
        /**
        * Run the database seeds.
        *
        * @return void
        */
        public function run()
        {
            \App\User::create('users')->insert([
                'name' => 'Admin',
                'email' => 'admin@admin.com',
                'password' => bcrypt('password'),
            ]);
        }
    }

Register seeder in `DatabaseSeeder`:

    <?php

    use Illuminate\Database\Seeder;

    class DatabaseSeeder extends Seeder
    {
        /**
        * Seed the application's database.
        *
        * @return void
        */
        public function run()
        {
            $this->call(UsersTableSeeder::class);
        }
    }

Finally you run seeder :

    php artisan db:seed

### Model Factories

Factories generate large amounts of database records. Laravel brings by default the `UserFactory` with the data to declare a user:
Laravel uses Faker that is a PHP library that generates fake data. [Read more](https://github.com/fzaninotto/Faker)

    <?php

    use Faker\Generator as Faker;


    $factory->define(App\User::class, function (Faker $faker) {
        return [
            'name' => $faker->name,
            'email' => $faker->unique()->safeEmail,
            'email_verified_at' => now(),
            'password' => '$2y$10$TKh8H1.PfQx37YgCzwiKb.KjNyWgaHb9cbcoQgdIVFlYg7B77UdFm', // secret
            'remember_token' => str_random(10),
        ];
    });

then you call factory in  `UserTableSeeder`. You can also specify the number of records:

    <?php

    use Illuminate\Database\Seeder;

    class UserTableSeeder extends Seeder
    {
        /**
        * Run the database seeds.
        *
        * @return void
        */
        public function run()
        {
            factory(App\User::class, 50)->create();
        }
    }

## Seeds and Factories with Relationships

Define relationship:

    public function up()
    {
        Schema::create('articles', function (Blueprint $table) {
            $table->increments('id');
            $table->string('title');
            $table->text('article_text');
            $table->unsignedInteger('user_id')->nullable();
            $table->foreign('user_id')->references('id')->on('users');
            $table->timestamps();
        });
    }

User factory:

    <?php

    use Faker\Generator as Faker;


    $factory->define(App\User::class, function (Faker $faker) {
        return [
            'name' => $faker->name,
            'email' => $faker->unique()->safeEmail,
            'email_verified_at' => now(),
            'password' => '$2y$10$TKh8H1.PfQx37YgCzwiKb.KjNyWgaHb9cbcoQgdIVFlYg7B77UdFm', // secret
            'remember_token' => str_random(10),
        ];
    });

Articles factory:

    <?php

    use Faker\Generator as Faker;


    $factory->define(App\User::class, function (Faker $faker) {
        return [
            'title' => $faker->text(50),
            'article_text' => $faker->text(500),
        ];
    });

In `UsertableSeeder` use saveMany method:

    <?php

    use Illuminate\Database\Seeder;

    class UserTableSeeder extends Seeder
    {
        /**
        * Run the database seeds.
        *
        * @return void
        */
        public function run()
        {
            factory(App\User::class, 50)->create()->each(function($user){
                $user->articles()->saveMany(factory(App\Article::class, 3)->make());
            });
        }
    }

## Check Methods/Properties in Eloquent API Docs 

In the documentation you will find all the information of the eloquent API and that you can work from the models.
a description, the methods and the type of value that they return, the parameters they receive and Traits available.

https://laravel.com/api/5.7/Illuminate/Database/Eloquent/Model.html

# Querying and Filtering Data Effectively

## Advanced find() and all(): Methods and Parameters 

`all(array|mixed $columns = ['*'])`
Get all of the models from the database.

    $user = User::all();
    $user = User::all(['name', 'id']);

`find(array|mixed $columns = ['*'])`
these methods return a single model instance.

    $user = User::find(1);
    $user = User::find(1, 2);
    $user = User::find([1, 2, 3], ['name']);

    $user = User::findOrFail(1);
    $user = User::where('email', 'example@mail.com')->firstOrFail();

## WhereX Magic Methods for Fields and Dates 

    $user = User::where('email', 'example@mail.com')->firstOrFail();
    $user = User::whereEmail('example@mail.com')->get();

    $user = User::where('created_at', '2019-12-27 11:28:29')->get();
    $user = User::whereDate('created_at', '2019-12-27')->get();
    $user = User::whereYear('created_at', '2019')->get();
    $user = User::whereMonth('created_at', '09')->get();
    $user = User::whereDay('created_at', '20')->get();
    $user = User::whereTime('created_at', '20:15:05')->get();
    $user = User::whereCreatedAt('20:15:05')->get();

    More wherre cluses: 
    whereBetween
    whereNotBetween
    whereIn / whereNotIn
    whereNull / whereNotNull
    whereDate / whereMonth / whereDay / whereYear / whereTime
    whereColumn

    https://laravel.com/docs/5.7/queries#where-clauses

 ## Brackets to Eloquent: (A and B) or (C and D) 

if you have and-or mix in SQL query, like this:

    public function index()
    {
        $articles = Article::where('user_id', 1)
        ->whereYear('created_at', 2018)
        ->orwhereYear('update_at', 2018)
        ->get();

        return view('articles.index', compact('articles'));
    }
You can display raw query sql with `toSql()` method:

    public function index()
    {
        $articles = Article::where('user_id', 1)
        ->whereYear('created_at', 2018)
        ->orwhereYear('update_at', 2018)
        ->toSql();
        dd($articles);

        return view('articles.index', compact('articles'));
    }

You have the follow result. The order will be incorrect.

    "select * from `articles` where `user_id` = ? and year(`created_at`) = ? or year(`updated_at`) = ?"

The right way is using closure functions as sub-queries:

    public function index()
    {
        $articles = Article::where('user_id', 1)
        ->where(function($query){
        return $query->whereYear('created_at', 2018)
            ->orwhereYear('update_at', 2018);
        })->get();

        return view('articles.index', compact('articles'));
    }

    public function index()
    {
        $articles = Article::where('user_id', 1)
        ->where(function($query){
        return $query->whereYear('created_at', 2018)
            ->orwhereYear('update_at', 2018);
        })->toSql();
        dd($articles);

        return view('articles.index', compact('articles'));
    }

Now, the result 

    "select * from `articles` where `user_id` = ? and (year(`created_at`) = ? or year(`updated_at`) = ?)"

## Query Scopes: Where Conditions Applied Globally

Global scopes allow you to add constraints to all queries for a given model.

    public function index()
    {
        $articles = Article::where('created_at', '>', now()->subDays(30)->get());
        return view('articles.index', compact('articles'));
    }

    public function search(Reques $request)
    {
        $articles = Article::where('created_at', '>', now()->subDays(30))
            ->where('user_id', $request->user_id)
            ->get();

        return view('articles.index', compact('articles'));
    }


    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Article extends Model
    {
        protected $fillable = ['title', 'article_text', 'user_id'];

        public function scopeNewest($query)
        {
            return $query->where('created_at', '>', now()->subDays(30));
        }
    }


    public function index()
    {
        $articles = Article::newest()->get());
        return view('articles.index', compact('articles'));
    }

    public function search(Reques $request)
    {
        $articles = Article::newest()
            ->where('user_id', $request->user_id)
            ->get();

        return view('articles.index', compact('articles'));
    }

Global scopes

    public function index()
    {
        $articles = Article::where('user_id', 1)->get());
        return view('articles.index', compact('articles'));
    }

    public function search(Reques $request)
    {
        $articles = Article::where('user_id', 1)
            ->where('user_id', $request->user_id)
            ->get();

        return view('articles.index', compact('articles'));
    }

    public function edit($article_id)
    {
        $article = Article::where('user_id', 1)
        ->find($article_id);
        return view('articles.index', compact('article'));
    }


    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Builder;

    class Article extends Model
    {
        /**
        * The "booting" method of the model.
        *
        * @return void
        */
        protected static function boot()
        {
            parent::boot();

            static::addGlobalScope('user_filter', function (Builder $builder) {
                $builder->where('user_id', 1);
            });
        }
    }


        public function index()
    {
        $articles = Article::all();
        return view('articles.index', compact('articles'));
    }

    public function search(Reques $request)
    {
        $articles = Article::where('user_id', $request->user_id)
            ->get();

        return view('articles.index', compact('articles'));
    }

    public function edit($article_id)
    {
        $article = Article::find($article_id);
        return view('articles.index', compact('article'));
    }


    <?php

    namespace App\Scopes;

    use Illuminate\Database\Eloquent\Scope;
    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Builder;

    class ArticleUserScope implements Scope
    {
        /**
        * Apply the scope to a given Eloquent query builder.
        *
        * @param  \Illuminate\Database\Eloquent\Builder  $builder
        * @param  \Illuminate\Database\Eloquent\Model  $model
        * @return void
        */
        public function apply(Builder $builder, Model $model)
        {
            $builder->where('user_id', 1);
        }
    }


    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Builder;

    class Article extends Model
    {
        /**
        * The "booting" method of the model.
        *
        * @return void
        */
        protected static function boot()
        {
            parent::boot();

            static::addGlobalScope(new ArticleUserScope);
        }
    }

## Eloquent when(): More Elegant if-statement 

if you have the following logic with if conditinal:

    <?php

    namespace App\Http\Controllers;

    use App\Article;
    use Illuminate\Http\Request;

    class ArticleController extends Controller
    {
        public function index()
        {
            $articles = Article::all();
            return view('articles.index', compact('articles'));
        }

        public function search()
        {
            $query = Article::query();
            if(request('user_id')){
                $query->where('user_id', request('user_id'));
            }
            if(request('title')){
                $query->where('title', request('title'));
            }
            $articles = $query->get();

            return view('articles.index', compact('articles'));
        }
    }

You can use the when method to replace the conditional if:

    <?php

    namespace App\Http\Controllers;

    use App\Article;
    use Illuminate\Http\Request;

    class ArticleController extends Controller
    {
        public function index()
        {
            $articles = Article::all();
            return view('articles.index', compact('articles'));
        }

        public function search()
        {
            $articles = Article::when(requet('user_id'), function($query){
                return $query->where('user_id', request('user_id'));
            })->when(request('title'), function($query){
                return $query->where('title', request('title'))
            })->get();


            return view('articles.index', compact('articles'));
        }
    }

## Ordering by Relationship: orderBy vs sortBy 

The orderBy method orders elements by the given key:

    $articles = Article::all()->orderBy("name");
    $articles = Article::orderBy('name')->get();

You can replace the `orderBy()` method by `shortBy()`:

        public function index()
        {
            $user = User::orderBy('name')->get();
            return view('users.index', compact('users'))
        }

You can use the collections with `all()` and use the sortBy method, by default `sortBy` orders the elements ascending:

        public function index()
        {
            $user = User::all()->sortBy('days_active');
            return view('users.index', compact('users'))
        }

to order the elements in descending order you use `sortByDesc()`:

        public function index()
        {
            $user = User::all()->sortByDesc('days_active');
            return view('users.index', compact('users'))
        }

## Raw Database Queries with Examples

To create a raw expression, you may use the DB::raw method:

    public function index()
    {
        $users = User::select(DB::raw('id, name, email, created_at, DATEDIFF(updated_at, created_at) as days_Active))->get();

        return view('users.index', compact('users'));
    }

    public function index()
    {
        $users = User::selectRaw('id, name, email, created_at, DATEDIFF(updated_at, created_at) as days_Active)->get();

        return view('users.index', compact('users'));
    }

    public function index()
    {
        $users = User::select(DB::raw('id, name, email, created_at, DATEDIFF(updated_at, created_at) as days_Active))
        ->whereRaw('DATEDIFF(updated_at, created_at) > 300')
        ->get();

        return view('users.index', compact('users'));
    }

    public function index()
    {
        $users = User::select(DB::raw('id, name, email, created_at, DATEDIFF(updated_at, created_at) as days_Active))
        ->orderByRaw('DATEDIFF(updated_at, created_at) desc')
        ->get();

        return view('users.index', compact('users'));
    }

# Eloquent Collections and their Methods

## Why You Need Collections and How to Use Them 

Laravel collections are one of the most powerful provisions of the Laravel framework. They are what PHP arrays should be, but better. (scotch.io)
The Eloquent collection object extends the Laravel base collection, so it naturally inherits dozens of methods used to fluently work with the underlying array of Eloquent models.

A small example:

    public function index()
    {
        $articles = Articles::all();

        $titles = [];
        foreach ($articles as $aticle){
            if(strlen($article->title) > 40){
                $titles[] = $article->title;
            }
        }

        dd($articles->filter(function($article){
            return strlen($article->title) > 40;
        })->map(function($article){
            return $article->title;
        }));

        return view('articles.index', compact('titles'));
    }

## Methods for Fetching and Transforming 

Some examples of the use of some collections methods:

Controller:

    public function index()
    {
        $articles = Article::all();
        return view('articles.index', compact('articles'));
    }

    public function create()
    {
        $users = User::select(['name', 'id'])->get()
        ->prepend(new User(['name' => '-- Please choose author --']));
        return view('articles.create', compact('users'));
    }

View:

    <select name="user_id" class="form-control">
        @foreach
            <option value="{{ $user->id }}">{{ $user->name }}</option>
        @endforeach
    </select>

The shuffle method randomly shuffles the items in the collection:

    $users = User::select(['name', 'id'])->get()->shuffle();

The pluck method retrieves all of the values for a given key:

    $users = User::pluck('name', 'id');

The chunk method breaks the collection into multiple, smaller collections of a given size:

    $users = User::select(['name', 'id'])->get()->shuffle()->chunk(3);

The random method returns a random item from the collection:

    $users = User::select(['name', 'id'])->get()->random();

The contains method determines whether the collection contains a given item:

    $users = User::select(['name', 'id'])->get()->random();
    if ($users->contains('password', '$2y$10$TydfRTyjLAVB834GnsaY'))
        dd('Not ready');

[More available methods](https://laravel.com/docs/5.7/collections#available-methods)

## Methods for Filtering with Callbacks

    public function index()
    {
        $users = User::all()->each(function($user) {
            if ($users->contains('password', '$2y$10$TydfRTyjLAVB834GnsaY')) {
                info('User ' . $user->email . 'has not changed password');
            }
        });

        $names = User::all()->map(function ($user) {
            return strlen($user->name);
        });

        $names = User::all()->filter(function ($user) {
            return strlen($user->name) > 17;
        });

        $names = User::all()->reject(function ($user) {
            return strlen($user->name) > 17;
        });
    }

 ## Methods for Math Calculations 

    public function index()
    {
        $articles = Article::all();
        echo 'Total articles' . $articles->count() . '<hr />';
        echo 'Total word written: ' . $articles->sum('word_count') . '<hr />';
        echo 'Minimun word count: ' . number_format($articles->min('word_count', 2)) . '<hr />';
        echo 'Maximun word count: ' . number_format($articles->max('word_count', 2)) . '<hr />';
        echo 'Average word count: ' . number_format($articles->avg('word_count', 2)) . '<hr />';
        echo 'Median word count: ' . number_format($articles->median('word_count', 2)) . '<hr />';
        echo 'Most often word count: ' . implode(', ' $articles->mode('word_count')) . '<hr />';
    }

Calculations:

count()
The count method returns the total number of items in the collection.

avg()
The avg method returns the average value of a given key.

max()
The max method returns the maximum value of a given key.

median()
The median method returns the median value of a given key.

min()
The min method returns the minimum value of a given key.

sum()
The sum method returns the sum of all items in the collection.

## Methods for Debugging

dd()
The dd method dumps the collection´s items and ends execution of the script.

dump()
The dump method dumps the collection´s items.

tap()
The tap method passes the collection to the given callback, allowing you to "tap" into the collection at a specific point and do something with the items.

    public function index()
    {
        $users = User::select(['name', 'id'])
            ->take(5)
            ->get()
            ->shuffle()
            ->chunk(3);
        dd($users);
    }

    public function index()
    {
        $users = User::select(['name', 'id'])
            ->take(5)
            ->get()
            ->shuffle()
            ->tap(function ($users) {
                info($users->first());
            })
            ->chunk(3);
    }

# Advanced Eloquent Relationships

## Polymorphic Relations Explained 

A polymorphic relationship allows the target model to belong to more than one type of model using a single association.

One To One (Polymorphic)

TABLES
migrations
photos
posts
products

| **Tables** |
|----------|
| migrations |
| photos |
| posts |
| products |


| **posts_photos** |
|----------|
| id |
| filename |
| post_id |
| timestamps |

| **products_photos** |
|----------|
| id  |
| filename |
| product_id |
| timestamps |

| **users_photos** |
|----------|
| id |
| filename |
| use_id |
| timestamps |

| **photos** |
|----------|
| id |
| filename |
| photoable_id |
| photoable_type |
| user_id |
| timestamps |

    Schema::create('photos', function (Blueprint $table) {
        $table->increments('id');
        $table->integer('imageable_id')->unsigned();
        $table->string('imageable_type');
        $table->string('filename');
        $table->timestamps();
    });

Photo model:

    class Photo extends model
    {
        protected $fillable = ['imageable_id', 'imageable_type', 'filename'];

        public function imageable()
        {
            return $this->morphTo();
        }
    }

Post model:

    class Post extends model
    {
        protected $fillable = ['title'];

        public function photos()
        {
            return $this->morphMany('App\Photo', 'imageable');
        }
    }

PostsController:

    public function store(Request $request)
    {
        $post = Post::create($request->only(['title']));
        $photos = explode(",", $request->get('photos')) ;
        foreach ($photos as $photo) {
            Photo::Create([
                'imageable_id' => $post->id,
                'imageable_type' => 'App\Post',
                'filename' => $photo
            ]);
        });
        return redirect()->route('posts.index');
    }

## Polymorphic Many-to-Many Relations 

One To Many (Polymorphic)

| **posts** |
|----------|
| id |
| title |

| **products** |
|----------|
| id |
| name |

| **photos** |
|----------|
| id |
| filename |

| **imageables**|
|---------|
| photo_id |
| imageable_id |
| imageable_type |

    Schema::create('imageables', function (Blueprint $table) {
        $table->unsignedInteger('photo_id');
        $table->foreign('photo_id')->references('id')->on('photos');
        $table->unsignedInteger('imageable_id');
        $table->string('imageable_type');
    });

Photo model:

    class Photo extends model
    {
        protected $fillable = ['filename'];

        public function products()
        {
            return $this->morphedByMany('App\Product', 'imageable');
        }

        public function posts()
        {
            return $this->morphedByMany('App\Post', 'imageable');
        }
    }

Product model:

    class Product extends model
    {
        protected $fillable = ['title'];

        public function photos()
        {
            return $this->morphedByMany('App\Photo', 'imageable');
        }
    }

Post model:

    class Post extends model
    {
        protected $fillable = ['title'];

        public function photos()
        {
            return $this->morphedByMany('App\Photo', 'imageable');
        }
    }

Imageable model:

    class Imageable extends model
    {
        public $timestamps = false;
        protected $fillable = ['photo_id', 'imageable_id', 'iamgeable_type'];
    }

PostController:

    public function store(Request $request)
    {
        $post = Post::create($request->only(['title']));
        $photos = explode(",", $request->get('photos')) ;
        foreach ($photos as $filename) {
            $photo = Photo::Create([
                'filename' => $filename
            ]);

            Imageable::create([
                'photo_id' => $photo->id
                'imageable_id' => $post->id,
                'imageable_type' => 'App\Post',
            ]);

        return redirect()->route('posts.index');
    }


## Advanced Pivot Tables in Many-to-Many 

    Schema::create('roles', function (Blueprint $table) {
        $table->increments('id');
        $table->string('name');
        $table->timestamps();
    });

    Schema::create('role_user', function (Blueprint $table) {
        $table->unsignedInteger('role_id');
        $table->foreign('role_id')->references('id')->on('roles');
        $table->unsignedInteger('user_id');
        $table->foreign('user_id')->references('id')->on('users');
        $table->boolen('approved')->default(0);
        $table->timestamps();
    });

    class User extends Authenticatable
    {
        use Notifiable;

        protected $fillable = [
            'name','email','password',
        ];

        protected $hidden = [
            'password','remember_token',
        ];

        public function roles()
        {
            return $this->belongsToMany(Role::class)->withTimestamps()->withPivot('approved');
        }

        public function approvedRoles()
        {
            return $this->belongsToMany(Role::class)->wherePivot('approved', 1);
        }
    }

`DatabaseSeeder`:

    public function run()
    {
        \App\Role::create(['name' => 'Administrator']);
        \App\Role::create(['name' => 'Editor']);
        \App\Role::create(['name' => 'Author']);

        $user = \App\User::Create([
            'name' => 'Administrator',
            'email' => admin@admin.com,
            'password' => bvrypt('password');
        ]);
        $user->roles()->attach(1, ['approved' => 1]);
        $user->roles()->attach(2);

        foreach($user->roles as $role) {
            //info($role->name . '(time '.$role->pivot->created_at', approved: '. $role->pivot->approved.')');
            info($role->name);
        }
    }

## HasManyThrough Relations 

    Schema::create('users', function (Blueprint $table) {
        $table->unsignedInteger('role_id');
        $table->foreign('role_id')->references('id')->on('roles');
        $table->string('name');
        $table->string('email')->unique();
        $table->timestamp('email_verified_at')->nullable();
        $table->string('password');
        $table->rememberToken();
        $table->timestamps();
    });

    Schema::create('roles', function (Blueprint $table) {
        $table->increments('id');
        $table->string('name');
        $table->timestamps();
    });

    Schema::create('posts', function (Blueprint $table) {
        $table->increments('id');
        $table->unsignedInteger('user_id');
        $table->foreign('user_id')->references('id')->on('users');
        $table->string('title');
        $table->text('post_text');
        $table->timestamps();
    });

User model:

    class User extends Authenticatable
    {
        use Notifiable;

        protected $fillable = [
            'name','email','password', 'role_id',
        ];

        protected $hidden = [
            'password','remember_token',
        ];

        public function role()
        {
            return $this->belongsTo(Role::class);
        }

        public function posts()
        {
            return $this->hasMany(Post::class);
        }
    }

Role model:

    class Role extends model
    {
        protected $fillable = ['name'];

        public function users()
        {
            return $this->hasMany(User::class);
        }

        public function posts()
        {
            return $this->hasManyThrough(Post::class, User::class);
        }
    }

Post model:

    class Post extends model
    {
        protected $fillable = ['user_id', 'title', 'post_text'];

        public function user()
        {
            return $this->belongsTo(User::class);
        }
    }

`DatabaseSeeder`:

    public function run()
    {
        \App\Role::create(['name' => 'Administrator']);
        \App\Role::create(['name' => 'Editor']);
        \App\Role::create(['name' => 'Author']);

        $user = \App\User::Create([
            'role_id' => 1,
            'name' => 'Administrator',
            'email' => admin@admin.com,
            'password' => bvrypt('password');
        ]);
        $user = \App\User::Create([
            'role_id' => 2,
            'name' => 'Editor',
            'email' => editor@editor.com,
            'password' => bvrypt('password');
        ]);
        $user = \App\User::Create([
            'role_id' => 3,
            'name' => 'Author',
            'email' => author@author.com,
            'password' => bvrypt('password');
        ]);

        for ($i=1; $i <= 10; $i++) {
            \App\Post::create([
                'user_id' => rand(1, 3),
                'title' => str_random(10),
                'post_text' => str_random(200),
            ]);
        }
    }

`HomeController`:

class HomeController extends Controller
{
    public function index()
    {
        $roles = Role::with('users.posts')->get();
        return view('home', compact('roles'));
    }
}

## Creating Records with Relationships 

    public function store(Request $request)
    {
        $author = Author::firstOrCreate(['name' => $request->author]);

        $titles = collect(explode(',', $request->titles))->map(function($record) {
            return ['title' => $record];
        })->toArray();

        $author->books()->createMany($titles);

        return redirect()->route('books.index');
    }

## Querying Records with Relationships

    class Book extends Model
    {
        protexted $fillable = ['author_id', 'title'];

        public function author()
        {
            return $this->belongsTo(Author::class);
        }

        public function ratings()
        {
            return $this->hasMany(Rating::class);
        }
    }

    public function index()
    {
        Author::whereHas('books', function($query){
            $query->where('title', 'like', '%b%');
        })->get()->dd();

        return view('books.index', compact('books'));
    }


# Eloquent Performance

## Laravel Debugbar: How to Measure Performance 

Installation:

    composer require barryvdh/laravel-debugbar --dev

Example:

    public function index()
    {
        $books = Book::with('author')
            ->where('title', 'like', '%a%')
            ->take(50)
            ->get();

        return view('books.index', compact('books'));
    }
    
Queries output in debugbar:

    select * from `books` where `title` like `%a%` limit 50 (1.46ms)

[Laravel Debugbar Github](https://github.com/barryvdh/laravel-debugbar)

## Performance Test: Eloquent vs Query Builder vs SQL

    public function test1()
    {
        $time_start = $this->microtime_float();

        $books = Book::with('author')
            ->where('title', 'like', '%a%')
            ->get();

        $time_end = $this->microtime_float();
        $time = $time_end - $time_start;

        return "Did nothing in $time seconds";
    }

    public function test2()
    {
        $time_start = $this->microtime_float();

        $books = \DB::table('books')
            ->join('authors', 'books.author_id', '=', 'authors.id')
            ->where('title', 'like', '%a%')
            ->get();

        $time_end = $this->microtime_float();
        $time = $time_end - $time_start;

        return "Did nothing in $time seconds";
    }

    public function test3()
    {
        $time_start = $this->microtime_float();

        $books = \DB::select("seelct * from books join authors on books.author_id = authors.id where title like %a%");

        $time_end = $this->microtime_float();
        $time = $time_end - $time_start;

        return "Did nothing in $time seconds";
    }

    private function microtime_float()
    {
        list($usec, $sec) = explode(" ", microtime());
        return ((float)$usec + (float)$sec);
    }

books/test1

    Did nothing in 0.40745592117310 seconds

books/test2
    
    Did nothing in 0.05786395072937 seconds

books/test3

    Did nothing in 0.07549003448486 seconds

## N+1 Problem and Eager Loading: Be Careful with Eloquent 

Controller:

    public function index()
    {
        $books = Book::where('title', 'like', '%a%')
            ->take(100)
            ->get();

        return view('books.index', compact('books'));
    }

view:

    @foreach ($books as $book)
        <tr>
            <td>{{ $book->title }}</td>
            <td>{{ $book->author->name }}</td>
        </tr>
    @endforeach

Laravel debugbar output:

    Queries 102 - 3.68s

Controller:

    public function index()
    {
        $books = Book::with('author')
            ->where('title', 'like', '%a%')
            ->take(100)
            ->get();

        return view('books.index', compact('books'));
    }

Laravel debugbar output:

    Queries 3 - 1.16s

[Laravel N+1 Query Detector](https://github.com/beyondcode/laravel-query-detector)

## Caching in Eloquent

    public function index()
    {
        $authors = Author::with('books')
        ->take(20)
        ->get();

        return view(books.index, compact('authors'));
    }

    public function getBooksCountAttribute()
    {
        return $this->books->count();
    }


Laravel Debugbar output:

    Queries 21 - 1.88s

You can use `Cache::remember` to caching the model for fifteen minutes. You can cache properties and associations on your models that are automatically updated (and the cache invalidated) when the model (or associated model) is updated.

Example:

    public function index()
    {
        $authors = Author->take(20)->get();

        return view(books.index, compact('authors'));
    }

    public function getBooksCountAttribute()
    {
        return Cache::remember('author-books-' . $this->id, 15, function(){
            return $this->books->count();
        });
    }

# Useful Packages to Extend Eloquent

## spatie/laravel-medialibrary: Associate files with Eloquent models 

Installation:

    composer require "spatie/laravel-medialibrary:^7.0.0"
    
You can publish the migration with:

    php artisan vendor:publish --provider="Spatie\MediaLibrary\MediaLibraryServiceProvider" --tag="migrations"

After the migration has been published you can create the media-table by running the migrations:

    php artisan migrate

This will create a media table:

    Schema::create('media', function (Blueprint $table) {
        $table->increments('id');
        $table->morphs('model');
        $table->string('collection_name');
        $table->string('name');
        $table->string('file_name');
        $table->string('mime_type')->nullable();
        $table->string('disk');
        $table->unsignedInteger('size');
        $table->json('manipulations');
        $table->json('custom_properties');
        $table->json('responsive_images');
        $table->unsignedInteger('order_column')->nullable();
        $table->nullableTimestamps();
    });

Create the symbolic link:

    php artisan storage:link

Create Book view:

    <form action="{{ route('books.store') }}" method="POST" enctype="multipart/form-data">
        @csrf

        Book title:
        <input type="text" class="form-control" name="title" />
        <br />

        Author:
        <select name="author_id" class="form-control">
            @foreach ($authors as $author)
                <option value="{{ $author->id }}">{{ $author->name }}</option>
            @endforeach
        </select>

        Cover image:
        <br />
        <input type="file" name="cover_image" />
        <br /><br />

        <input type="submit" value="Save book" />
    </form>

This should look like this:

<img width="1680" alt="Login" src="medialibrary.png">

Book model:

    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;
    use Spatie\MediaLibrary\HasMedia\HasMediaTrait;
    use Spatie\MediaLibrary\HasMedia\HasMedia;
    use Spatie\MediaLibrary\Models\Media;

    class Book extends Model implements HasMedia
    {
        use HasMediaTrait;

        protected $fillable = ['author_id', 'title'];

        public function author()
        {
            return $this->belongsTo(Author::class);
        }

        public function registerMediaConversions(Media $media = null)
        {
            $this->addMediaConversion('thumb')
                ->width(100)
                ->height(100);
        }
    }

BookController:

    <?php

    namespace App\Http\Controllers;

    use App\Book;
    use App\Author;
    use Illuminate\Http\Request;

    class BookController extends Controller
    {
        public function index()
        {
            $books = Book::with('author')->get();
            return view('books.index', compact('books'));
        }

        public function create()
        {
            $authors = Author::all();
            return view('books.create', compact('authors'));
        }

        public function store(Request $request)
        {
            $book = Book::create($request->all());

            if ($request->hasFile('cover_image')) {
                $book->addMediaFromRequest('cover_image')->toMediaCollection('cover_images');
            }

            return redirect()->route('books.index');
        }
    }


Index book view:

    <tbody>
        @foreach ($books as $book)
            <tr>
                <td>{{ $book->title }}</td>
                <td>{{ $book->author->name }}</td>
                <td>
                    <img src="{{ $book->getFirstMediaUrl('cover_images') }}">
                </td>
                </tr>
        @endforeach
    </tbody>

This should look like this:

<img width="1680" alt="Login" src="fullpath.png"> 

Index book view by adding the second parameter to `getFirstMediaUrl`:

    <tbody>
        @foreach ($books as $book)
            <tr>
                <td>{{ $book->title }}</td>
                <td>{{ $book->author->name }}</td>
                <td>
                    <img src="{{ $book->getFirstMediaUrl('cover_images', 'thumb') }}">
                </td>
                </tr>
        @endforeach
    </tbody>

This should look like this:

<img width="1680" alt="Login" src="thumb.png">   

[Associate files with Eloquent models - Github](https://github.com/spatie/laravel-medialibrary)

## dimsav/laravel-translatable: Package for Multilingual Models

    composer require dimsav/laravel-translatable

    php artisan make:model ArticleTranslation -m


    Schema::create('article_translations', function(Blueprint $table)
    {
        $table->increments('id');
        $table->integer('country_id')->unsigned();
        $table->string('name');
        $table->string('locale')->index();

        $table->unique(['country_id','locale']);
        $table->foreign('country_id')->references('id')->on('countries')->onDelete('cascade');
    });

 Configuration:

    php artisan vendor:publish --tag=translatable

Install laravel Collective:

    composer require "laravelcollective/html":"^5.4.0"

Article model:

    <?php

    namespace App;

    use Dimsav\Translatable\Translatable;
    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\SoftDeletes;

    class Article extends Model
    {
        use SoftDeletes;
        use Translatable;

        protected $fillable = ['title', 'article_text'];
        public $translatedAttributes = ['title', 'article_text'];
    }

ArticleTranslation model:

    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class ArticleTranslation extends Model
    {
        public $timestamps = false;
        protected $fillable = ['title', 'article_text'];
    }

create view:

   {!! Form::open(['method' => 'POST', 'route' => ['admin.articles.store']]) !!}

    <div class="panel panel-default">
        <div class="panel-heading">
            @lang('global.app_create')
        </div>

        <div class="panel-body">
            <div class="row">
                <div class="col-xs-12 form-group">
                    {!! Form::label('en_title', trans('global.articles.title').' [EN]', ['class' => 'control-label']) !!}
                    {!! Form::text('en_title', old('en_title'), ['class' => 'form-control', 'placeholder' => '']) !!}
                    <p class="help-block"></p>
                    @if($errors->has('en_title'))
                        <p class="help-block">
                            {{ $erros->first('en_title') }}
                        </p>
                    @endif
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 form-group">
                    {!! Form::label('en_article_text', trans('global.articles.title').' [EN]', ['class' => 'control-label']) !!}
                    {!! Form::text('en_article_text', old('en_article_text'), ['class' => 'form-control', 'placeholder' => '']) !!}
                    <p class="help-block"></p>
                    @if($errors->has('en_article_text'))
                        <p class="help-block">
                            {{ $erros->first('en_article_text') }}
                        </p>
                    @endif
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 form-group">
                    {!! Form::label('es_title', trans('global.articles.title').' [ES]', ['class' => 'control-label']) !!}
                    {!! Form::text('es_title', old('es_title'), ['class' => 'form-control', 'placeholder' => '']) !!}
                    <p class="help-block"></p>
                    @if($errors->has('es_title'))
                        <p class="help-block">
                            {{ $erros->first('es_title') }}
                        </p>
                    @endif
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 form-group">
                    {!! Form::label('es_article_text', trans('global.articles.title').' [ES]', ['class' => 'control-label']) !!}
                    {!! Form::text('es_article_text', old('es_article_text'), ['class' => 'form-control', 'placeholder' => '']) !!}
                    <p class="help-block"></p>
                    @if($errors->has('es_article_text'))
                        <p class="help-block">
                            {{ $erros->first('es_article_text') }}
                        </p>
                    @endif
                </div>
            </div>

ArticlesController:

    public function store(StoreArticlesRequest $request)
    {
        if(! Gate::allows('article_create')){
            return abort(401);
        }
        Article::create(
            [
                'en' => [
                    'title' => $request->en_title,
                    'article_text' => $request->en_article_text
                ],
                'es' => [
                    'title' => $request->es_title,
                    'article_text' => $request->es_article_text
                ]
            ]
        );
        return redirect()->route('admin.articles.index');
    }


`app.php`:

    /*
    |--------------------------------------------------------------------------
    | Application Locale Configuration
    |--------------------------------------------------------------------------
    |
    | The application locale determines the default locale that will be used
    | by the translation service provider. You are free to set this value
    | to any of the locales which will be supported by the application.
    |
    */

    'locale' => 'en',

to translate any field we use the translate method:

    {{ $article->translate('es')->title }}

[A Laravel package for multilingual models](https://github.com/dimsav/laravel-translatable)

### Defining Relationship
 - [Artisan Command make:model with (hidden) options](#artisan-command-makemodel-with-hidden-options) 


# Class Curriculum - laraveldaily (26 Dec 2018)

## Eloquent Model Options and Settings
 - [Artisan Command make:model with (hidden) options](#artisan-command-makemodel-with-hidden-options)
 - [Singular or Plural? What about multiple words?](#singular-or-plural-what-about-multiple-words)
 - [Saving a Model: $fillable or $guarded?](#saving-a-model-fillable-or-guarded)
 - [Properties for Tables, Keys, Increments, Pages and Dates](#properties-for-tables-keys-increments-pages-and-dates)

## Create/Update in Eloquent
 -  ["Magic" methods: FirstOrCreate() and other 2-in-1s](#magic-methods-firstorcreate-and-other-2-in-1s)
 -  [Model Observers: "listening" to record changes](#model-observers-listening-to-record-changes)
 -  [Accessors and Mutators: Change Model Values](#accessors-and-mutators-change-model-values)
 -  [Database Seeds and Factories: Prepare Dummy Data](#database-seeds-and-factories-prepare-dummy-data)
 -  [Seeds and Factories with Relationships](#seeds-and-factories-with-relationships)
 -  [Check Methods/Properties in Eloquent API Docs](#check-methodsproperties-in-eloquent-api-docs)


## Querying and Filtering Data Effectively
 -  [Advanced find() and all(): Methods and Parameters](#advanced-find-and-all-methods-and-parameters)
 -  [WhereX Magic Methods for Fields and Dates](#wherex-magic-methods-for-fields-and-dates)
 -  [Brackets to Eloquent: (A and B) or (C and D)](#brackets-to-eloquent-a-and-b-or-c-and-d)
 -  [Query Scopes: Where Conditions Applied Globally](#query-scopes-where-conditions-applied-globally)
 -  [Eloquent when(): More Elegant if-statement](#eloquent-when-more-elegant-if-statement)
 -  [Ordering by Relationship: orderBy vs sortBy](#ordering-by-relationship-orderby-vs-sortby)
 -  [Raw Database Queries with Examples](#raw-database-queries-with-examples)


## Eloquent Collections and their Methods
 - [Why You Need Collections and How to Use Them](#why-you-need-collections-and-how-to-use-them)
 - [Methods for Fetching and Transforming](#methods-for-fetching-and-transforming)
 - [Methods for Filtering with Callbacks](#methods-for-filtering-with-callbacks)
 - [Methods for Math Calculations](#methods-for-math-calculations)
 - [Methods for Debugging](#methods-for-debugging)
|

## Advanced Eloquent Relationships
 - [Polymorphic Relations Explained](#polymorphic-relations-explained)
 - [Polymorphic Many-to-Many Relations](#polymorphic-many-to-many-relations)
 - [Advanced Pivot Tables in Many-to-Many](#advanced-pivot-tables-in-many-to-many)
 - [HasManyThrough Relations](#hasmanythrough-relations)
 - [Creating Records with Relationships](#creating-records-with-relationships)
 - [Querying Records with Relationships](#querying-records-with-relationships)


## Eloquent Performance
 - [Laravel Debugbar: How to Measure Performance](#laravel-debugbar-how-to-measure-performance)
 - [Performance Test: Eloquent vs Query Builder vs SQL](#performance-test-eloquent-vs-query-builder-vs-sql)
 - [N+1 Problem and Eager Loading: Be Careful with Eloquent](#n1-problem-and-eager-loading-be-careful-with-eloquent)
 - [Caching in Eloquent](#caching-in-eloquent)


## Useful Packages to Extend Eloquent
 - [spatie/laravel-medialibrary: Associate files with Eloquent models](#spatielaravel-medialibrary-associate-files-with-eloquent-models)
 - [dimsav/laravel-translatable: Package for Multilingual Models](#dimsavlaravel-translatable-package-for-multilingual-models)
 - [spatie/eloquent-sortable: Sortable Eloquent Models](https://github.com/spatie/eloquent-sortable)
 - [spatie/laravel-tags: Add Tags and Taggable Behavior](https://github.com/spatie/laravel-tags)
 - [owen-it/laravel-auditing: Record the Changes From Models](https://github.com/owen-it/laravel-auditing)
 - [michaeldyrynda/laravel-cascade-soft-deletes: Cascade Delete & Restore](https://github.com/michaeldyrynda/laravel-cascade-soft-deletes)

# Eloquent Model Options and Settings

## Artisan Command make:model with (hidden) options 

 Create a model instance:
 
    php artisan make:model Post

 Create a model instance with migration:

    php artisan make:model Post --migration
    php artisan make:model Post -m

 Create a model instance with migration and controller:

     php artisan make:model Post -mc

 Create a model instance with migration and resource controller:

     php artisan make:model Post -mcr

 Create a model instance with migration,resource controller and factory:

    php artisan make:model Post -mcrf

Shorcut to create a model instance with migration,resource controller and factory:

    php artisan make:model Post -a

Display and describe the command's available arguments and options:

    php artisan make:model --help


## Singular or Plural? What about multiple words?

What | How | Good | Bad
------------ | ------------- | ------------- | -------------
Controller | singular | ArticleController | ~~ArticlesController~~
Model | singular | User | ~~Users~~
Table | plural | article_comments | ~~article_comment, articleComments~~
Migration | - | 2017_01_01_000000_create_articles_table | ~~2017_01_01_000000_articles~~

Read more naming conventions [Laravel best practices](https://github.com/alexeymezenin/laravel-best-practices/blob/master/README.md#follow-laravel-naming-conventions)


## Saving a Model: $fillable or $guarded? 

Mass assignment: means to send an array to the model to directly create a new record in Database.

$fillable specifies which attributes in the table should be mass-assignable.

    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Article extends Model
    {
        /**
        * The attributes that are mass assignable.
        *
        * @var array
        */
        protected $fillable = ['title', 'article_text'];
    }

$guarded specifies which attributes in the table shouldn't be mass-assignable.
    
    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Article extends Model
    {
        /**
        * The attributes that are mass assignable.
        *
        * @var array
        */
        protected $guarded = ['id'];
    }

## Properties for Tables, Keys, Increments, Pages and Dates 

`$table` specifies a custom table.

`$primaryKey` specifies a custom primary key. 

`$incrementing` specifies a non-incrementing or a non-numeric primary key.

`$perPage` specifies the number of items per page in paginate.

`$timestamps` disable created_at and updated_at columns.

`CREATED_AT` and `UPDATED_AT` specify the custom names of the columns used to store the timestamps.

`$dateFormat` specifies the custom format of your timestamps.

`$dates` converts columns to instances of Carbon.

    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Article extends Model
    {
        /**
        * The attributes that are mass assignable.
        *
        * @var array
        */
        protected $table = 'user_articles';

        protected $primaryKey = 'article_id';

        public $incrementing = false;

        $perPage = 5;

        public $timestamps = false;

        const CREATED_AT = 'creation_date';

        const UPDATED_AT = 'last_update';

        protected $dateFormat = 'm/d/Y H:i:s';

        protected $dates = [
            'created_at',
            'updated_at',
            'deleted_at'
        ];
                
    }

# Create/Update in Eloquent

## "Magic" methods: FirstOrCreate() and other 2-in-1s

There are two other methods you may use to create models by mass assigning attributes:  firstOrCreate and firstOrNew. The firstOrCreate method will attempt to locate a database record using the given column / value pairs. If the model can not be found in the database, a record will be inserted with the attributes from the first parameter, along with those in the optional second parameter. [Laravel docs](https://laravel.com/docs/5.7/eloquent#other-creation-methods)

    function store(Request $request)
    {
        $article = Article::where('title', $request->title)->first();
        if(!$article){
            $article = Article::create([
                'title' => $request->title,
                'article_text' => $request->article_text
            ]);
        }

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

It can be replaced by:

    function store(Request $request)
    {
        $article = Article::firstOrCreate(['title' => $request->title], ['article_text' => $request->article_text]);

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

    function store(Request $request)
    {
        $article = Article::firstOrNew(['title' => $request->title], ['article_text' => $request->article_text]);
        $article->field = $value;
        $article->save();

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

`updateOrCreate` updates an existing model or create a new model if none exists.

    function store(Request $request)
    {
        $article = Article::where('title', $request->title)->where('user_id', auth()->id()->first();
        if($article){
            $article->update(['article_text' => $request-article_text]);
        }else{
            $article = Article::create([
                'title' => $request->title,
                'article_text' => $request->article_text.
                'user_id' => auth()->id
            ]);
        }

        $article = Article::updateOrCreate(['title' => $request->title, 'user_id' => auth()->id()]);

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

It can be replaced by:

        function store(Request $request)
    {
        $article = Article::updateOrCreate(['title' => $request->title, 'user_id' => auth()->id()],
        ['article_text' => $request->article_text]);

        // some actions with the article
        $article->chapters()->create($request->chapters);
    }

## Model Observers: "listening" to record changes 

Observers are used to group event listeners for a model, for create a new observer run:

    php artisan make:observer ArticleObserver --model=Article

Register the observer in the `AppServiceProvider`:

    <?php

    namespace App\Providers;

    use App\Article;
    use App\Observers\UserObserver;
    use Illuminate\Support\ServiceProvider;

    class AppServiceProvider extends ServiceProvider
    {
        /**
        * Bootstrap any application services.
        *
        * @return void
        */
        public function boot()
        {
            Article::observe(ArticleObserver::class);
        }

        /**
        * Register the service provider.
        *
        * @return void
        */
        public function register()
        {
            //
        }
    }

Article model:

    public function store(Request $request)
    {
        Article::create($request->all());
        return redirect()->route('articles.index');
    }

ArticleObserver:

    public function createdArticle(Article $article)
    {
        info('Article is saved');
    }

Every time an article is created, you will have a message in log.

    [2018-09-19 20:15:26] local.INFO: Article is saved

## Accessors and Mutators: Change Model Values 

Accessors and mutators allow you to format Eloquent attribute values when you retrieve or set them on model instances. 

Accesor -> get Attribute
Mutator -> set Attribute

Create a `getFullNameAttribute` method on model:

    public function getFullNameAttribute()
    {
        return $this->name . ' ' . $this->surname;
    }

To access the value of the accessor, you may access the  `first_name` attribute on a model instance:

    <td>{{ $user->full_name }}</td>


    public function setNameAttribute($value)
    {
        $this->attributes['name'] = ucfirst($value);
    }

to set the first_name attribute to Taylor:

    $user->first_name = 'taylor';

## Database Seeds and Factories: Prepare Dummy Data

### Seeders

Seeding your database with test data using seed classes. Create seeder run:

    php artisan make:seeder UsersTableSeeder

add a database insert statement to the run method:

    <?php

    use Illuminate\Database\Seeder;

    class UserTableSeeder extends Seeder
    {
        /**
        * Run the database seeds.
        *
        * @return void
        */
        public function run()
        {
            \App\User::create('users')->insert([
                'name' => 'Admin',
                'email' => 'admin@admin.com',
                'password' => bcrypt('password'),
            ]);
        }
    }

Register seeder in `DatabaseSeeder`:

    <?php

    use Illuminate\Database\Seeder;

    class DatabaseSeeder extends Seeder
    {
        /**
        * Seed the application's database.
        *
        * @return void
        */
        public function run()
        {
            $this->call(UsersTableSeeder::class);
        }
    }

Finally you run seeder :

    php artisan db:seed

### Model Factories

Factories generate large amounts of database records. Laravel brings by default the `UserFactory` with the data to declare a user:
Laravel uses Faker that is a PHP library that generates fake data. [Read more](https://github.com/fzaninotto/Faker)

    <?php

    use Faker\Generator as Faker;


    $factory->define(App\User::class, function (Faker $faker) {
        return [
            'name' => $faker->name,
            'email' => $faker->unique()->safeEmail,
            'email_verified_at' => now(),
            'password' => '$2y$10$TKh8H1.PfQx37YgCzwiKb.KjNyWgaHb9cbcoQgdIVFlYg7B77UdFm', // secret
            'remember_token' => str_random(10),
        ];
    });

then you call factory in  `UserTableSeeder`. You can also specify the number of records:

    <?php

    use Illuminate\Database\Seeder;

    class UserTableSeeder extends Seeder
    {
        /**
        * Run the database seeds.
        *
        * @return void
        */
        public function run()
        {
            factory(App\User::class, 50)->create();
        }
    }

## Seeds and Factories with Relationships

Define relationship:

    public function up()
    {
        Schema::create('articles', function (Blueprint $table) {
            $table->increments('id');
            $table->string('title');
            $table->text('article_text');
            $table->unsignedInteger('user_id')->nullable();
            $table->foreign('user_id')->references('id')->on('users');
            $table->timestamps();
        });
    }

User factory:

    <?php

    use Faker\Generator as Faker;


    $factory->define(App\User::class, function (Faker $faker) {
        return [
            'name' => $faker->name,
            'email' => $faker->unique()->safeEmail,
            'email_verified_at' => now(),
            'password' => '$2y$10$TKh8H1.PfQx37YgCzwiKb.KjNyWgaHb9cbcoQgdIVFlYg7B77UdFm', // secret
            'remember_token' => str_random(10),
        ];
    });

Articles factory:

    <?php

    use Faker\Generator as Faker;


    $factory->define(App\User::class, function (Faker $faker) {
        return [
            'title' => $faker->text(50),
            'article_text' => $faker->text(500),
        ];
    });

In `UsertableSeeder` use saveMany method:

    <?php

    use Illuminate\Database\Seeder;

    class UserTableSeeder extends Seeder
    {
        /**
        * Run the database seeds.
        *
        * @return void
        */
        public function run()
        {
            factory(App\User::class, 50)->create()->each(function($user){
                $user->articles()->saveMany(factory(App\Article::class, 3)->make());
            });
        }
    }

## Check Methods/Properties in Eloquent API Docs 

In the documentation you will find all the information of the eloquent API and that you can work from the models.
a description, the methods and the type of value that they return, the parameters they receive and Traits available.

https://laravel.com/api/5.7/Illuminate/Database/Eloquent/Model.html

# Querying and Filtering Data Effectively

## Advanced find() and all(): Methods and Parameters 

`all(array|mixed $columns = ['*'])`
Get all of the models from the database.

    $user = User::all();
    $user = User::all(['name', 'id']);

`find(array|mixed $columns = ['*'])`
these methods return a single model instance.

    $user = User::find(1);
    $user = User::find(1, 2);
    $user = User::find([1, 2, 3], ['name']);

    $user = User::findOrFail(1);
    $user = User::where('email', 'example@mail.com')->firstOrFail();

## WhereX Magic Methods for Fields and Dates 

    $user = User::where('email', 'example@mail.com')->firstOrFail();
    $user = User::whereEmail('example@mail.com')->get();

    $user = User::where('created_at', '2019-12-27 11:28:29')->get();
    $user = User::whereDate('created_at', '2019-12-27')->get();
    $user = User::whereYear('created_at', '2019')->get();
    $user = User::whereMonth('created_at', '09')->get();
    $user = User::whereDay('created_at', '20')->get();
    $user = User::whereTime('created_at', '20:15:05')->get();
    $user = User::whereCreatedAt('20:15:05')->get();

    More wherre cluses: 
    whereBetween
    whereNotBetween
    whereIn / whereNotIn
    whereNull / whereNotNull
    whereDate / whereMonth / whereDay / whereYear / whereTime
    whereColumn

    https://laravel.com/docs/5.7/queries#where-clauses

 ## Brackets to Eloquent: (A and B) or (C and D) 

if you have and-or mix in SQL query, like this:

    public function index()
    {
        $articles = Article::where('user_id', 1)
        ->whereYear('created_at', 2018)
        ->orwhereYear('update_at', 2018)
        ->get();

        return view('articles.index', compact('articles'));
    }
You can display raw query sql with `toSql()` method:

    public function index()
    {
        $articles = Article::where('user_id', 1)
        ->whereYear('created_at', 2018)
        ->orwhereYear('update_at', 2018)
        ->toSql();
        dd($articles);

        return view('articles.index', compact('articles'));
    }

You have the follow result. The order will be incorrect.

    "select * from `articles` where `user_id` = ? and year(`created_at`) = ? or year(`updated_at`) = ?"

The right way is using closure functions as sub-queries:

    public function index()
    {
        $articles = Article::where('user_id', 1)
        ->where(function($query){
        return $query->whereYear('created_at', 2018)
            ->orwhereYear('update_at', 2018);
        })->get();

        return view('articles.index', compact('articles'));
    }

    public function index()
    {
        $articles = Article::where('user_id', 1)
        ->where(function($query){
        return $query->whereYear('created_at', 2018)
            ->orwhereYear('update_at', 2018);
        })->toSql();
        dd($articles);

        return view('articles.index', compact('articles'));
    }

Now, the result 

    "select * from `articles` where `user_id` = ? and (year(`created_at`) = ? or year(`updated_at`) = ?)"

## Query Scopes: Where Conditions Applied Globally

Global scopes allow you to add constraints to all queries for a given model.

    public function index()
    {
        $articles = Article::where('created_at', '>', now()->subDays(30)->get());
        return view('articles.index', compact('articles'));
    }

    public function search(Reques $request)
    {
        $articles = Article::where('created_at', '>', now()->subDays(30))
            ->where('user_id', $request->user_id)
            ->get();

        return view('articles.index', compact('articles'));
    }


    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class Article extends Model
    {
        protected $fillable = ['title', 'article_text', 'user_id'];

        public function scopeNewest($query)
        {
            return $query->where('created_at', '>', now()->subDays(30));
        }
    }


    public function index()
    {
        $articles = Article::newest()->get());
        return view('articles.index', compact('articles'));
    }

    public function search(Reques $request)
    {
        $articles = Article::newest()
            ->where('user_id', $request->user_id)
            ->get();

        return view('articles.index', compact('articles'));
    }

Global scopes

    public function index()
    {
        $articles = Article::where('user_id', 1)->get());
        return view('articles.index', compact('articles'));
    }

    public function search(Reques $request)
    {
        $articles = Article::where('user_id', 1)
            ->where('user_id', $request->user_id)
            ->get();

        return view('articles.index', compact('articles'));
    }

    public function edit($article_id)
    {
        $article = Article::where('user_id', 1)
        ->find($article_id);
        return view('articles.index', compact('article'));
    }


    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Builder;

    class Article extends Model
    {
        /**
        * The "booting" method of the model.
        *
        * @return void
        */
        protected static function boot()
        {
            parent::boot();

            static::addGlobalScope('user_filter', function (Builder $builder) {
                $builder->where('user_id', 1);
            });
        }
    }


        public function index()
    {
        $articles = Article::all();
        return view('articles.index', compact('articles'));
    }

    public function search(Reques $request)
    {
        $articles = Article::where('user_id', $request->user_id)
            ->get();

        return view('articles.index', compact('articles'));
    }

    public function edit($article_id)
    {
        $article = Article::find($article_id);
        return view('articles.index', compact('article'));
    }


    <?php

    namespace App\Scopes;

    use Illuminate\Database\Eloquent\Scope;
    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Builder;

    class ArticleUserScope implements Scope
    {
        /**
        * Apply the scope to a given Eloquent query builder.
        *
        * @param  \Illuminate\Database\Eloquent\Builder  $builder
        * @param  \Illuminate\Database\Eloquent\Model  $model
        * @return void
        */
        public function apply(Builder $builder, Model $model)
        {
            $builder->where('user_id', 1);
        }
    }


    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\Builder;

    class Article extends Model
    {
        /**
        * The "booting" method of the model.
        *
        * @return void
        */
        protected static function boot()
        {
            parent::boot();

            static::addGlobalScope(new ArticleUserScope);
        }
    }

## Eloquent when(): More Elegant if-statement 

if you have the following logic with if conditinal:

    <?php

    namespace App\Http\Controllers;

    use App\Article;
    use Illuminate\Http\Request;

    class ArticleController extends Controller
    {
        public function index()
        {
            $articles = Article::all();
            return view('articles.index', compact('articles'));
        }

        public function search()
        {
            $query = Article::query();
            if(request('user_id')){
                $query->where('user_id', request('user_id'));
            }
            if(request('title')){
                $query->where('title', request('title'));
            }
            $articles = $query->get();

            return view('articles.index', compact('articles'));
        }
    }

You can use the when method to replace the conditional if:

    <?php

    namespace App\Http\Controllers;

    use App\Article;
    use Illuminate\Http\Request;

    class ArticleController extends Controller
    {
        public function index()
        {
            $articles = Article::all();
            return view('articles.index', compact('articles'));
        }

        public function search()
        {
            $articles = Article::when(requet('user_id'), function($query){
                return $query->where('user_id', request('user_id'));
            })->when(request('title'), function($query){
                return $query->where('title', request('title'))
            })->get();


            return view('articles.index', compact('articles'));
        }
    }

## Ordering by Relationship: orderBy vs sortBy 

The orderBy method orders elements by the given key:

    $articles = Article::all()->orderBy("name");
    $articles = Article::orderBy('name')->get();

You can replace the `orderBy()` method by `shortBy()`:

        public function index()
        {
            $user = User::orderBy('name')->get();
            return view('users.index', compact('users'))
        }

You can use the collections with `all()` and use the sortBy method, by default `sortBy` orders the elements ascending:

        public function index()
        {
            $user = User::all()->sortBy('days_active');
            return view('users.index', compact('users'))
        }

to order the elements in descending order you use `sortByDesc()`:

        public function index()
        {
            $user = User::all()->sortByDesc('days_active');
            return view('users.index', compact('users'))
        }

## Raw Database Queries with Examples

To create a raw expression, you may use the DB::raw method:

    public function index()
    {
        $users = User::select(DB::raw('id, name, email, created_at, DATEDIFF(updated_at, created_at) as days_Active))->get();

        return view('users.index', compact('users'));
    }

    public function index()
    {
        $users = User::selectRaw('id, name, email, created_at, DATEDIFF(updated_at, created_at) as days_Active)->get();

        return view('users.index', compact('users'));
    }

    public function index()
    {
        $users = User::select(DB::raw('id, name, email, created_at, DATEDIFF(updated_at, created_at) as days_Active))
        ->whereRaw('DATEDIFF(updated_at, created_at) > 300')
        ->get();

        return view('users.index', compact('users'));
    }

    public function index()
    {
        $users = User::select(DB::raw('id, name, email, created_at, DATEDIFF(updated_at, created_at) as days_Active))
        ->orderByRaw('DATEDIFF(updated_at, created_at) desc')
        ->get();

        return view('users.index', compact('users'));
    }

# Eloquent Collections and their Methods

## Why You Need Collections and How to Use Them 

Laravel collections are one of the most powerful provisions of the Laravel framework. They are what PHP arrays should be, but better. (scotch.io)
The Eloquent collection object extends the Laravel base collection, so it naturally inherits dozens of methods used to fluently work with the underlying array of Eloquent models.

A small example:

    public function index()
    {
        $articles = Articles::all();

        $titles = [];
        foreach ($articles as $aticle){
            if(strlen($article->title) > 40){
                $titles[] = $article->title;
            }
        }

        dd($articles->filter(function($article){
            return strlen($article->title) > 40;
        })->map(function($article){
            return $article->title;
        }));

        return view('articles.index', compact('titles'));
    }

## Methods for Fetching and Transforming 

Some examples of the use of some collections methods:

Controller:

    public function index()
    {
        $articles = Article::all();
        return view('articles.index', compact('articles'));
    }

    public function create()
    {
        $users = User::select(['name', 'id'])->get()
        ->prepend(new User(['name' => '-- Please choose author --']));
        return view('articles.create', compact('users'));
    }

View:

    <select name="user_id" class="form-control">
        @foreach
            <option value="{{ $user->id }}">{{ $user->name }}</option>
        @endforeach
    </select>

The shuffle method randomly shuffles the items in the collection:

    $users = User::select(['name', 'id'])->get()->shuffle();

The pluck method retrieves all of the values for a given key:

    $users = User::pluck('name', 'id');

The chunk method breaks the collection into multiple, smaller collections of a given size:

    $users = User::select(['name', 'id'])->get()->shuffle()->chunk(3);

The random method returns a random item from the collection:

    $users = User::select(['name', 'id'])->get()->random();

The contains method determines whether the collection contains a given item:

    $users = User::select(['name', 'id'])->get()->random();
    if ($users->contains('password', '$2y$10$TydfRTyjLAVB834GnsaY'))
        dd('Not ready');

[More available methods](https://laravel.com/docs/5.7/collections#available-methods)

## Methods for Filtering with Callbacks

    public function index()
    {
        $users = User::all()->each(function($user) {
            if ($users->contains('password', '$2y$10$TydfRTyjLAVB834GnsaY')) {
                info('User ' . $user->email . 'has not changed password');
            }
        });

        $names = User::all()->map(function ($user) {
            return strlen($user->name);
        });

        $names = User::all()->filter(function ($user) {
            return strlen($user->name) > 17;
        });

        $names = User::all()->reject(function ($user) {
            return strlen($user->name) > 17;
        });
    }

 ## Methods for Math Calculations 

    public function index()
    {
        $articles = Article::all();
        echo 'Total articles' . $articles->count() . '<hr />';
        echo 'Total word written: ' . $articles->sum('word_count') . '<hr />';
        echo 'Minimun word count: ' . number_format($articles->min('word_count', 2)) . '<hr />';
        echo 'Maximun word count: ' . number_format($articles->max('word_count', 2)) . '<hr />';
        echo 'Average word count: ' . number_format($articles->avg('word_count', 2)) . '<hr />';
        echo 'Median word count: ' . number_format($articles->median('word_count', 2)) . '<hr />';
        echo 'Most often word count: ' . implode(', ' $articles->mode('word_count')) . '<hr />';
    }

Calculations:

count()
The count method returns the total number of items in the collection.

avg()
The avg method returns the average value of a given key.

max()
The max method returns the maximum value of a given key.

median()
The median method returns the median value of a given key.

min()
The min method returns the minimum value of a given key.

sum()
The sum method returns the sum of all items in the collection.

## Methods for Debugging

dd()
The dd method dumps the collection´s items and ends execution of the script.

dump()
The dump method dumps the collection´s items.

tap()
The tap method passes the collection to the given callback, allowing you to "tap" into the collection at a specific point and do something with the items.

    public function index()
    {
        $users = User::select(['name', 'id'])
            ->take(5)
            ->get()
            ->shuffle()
            ->chunk(3);
        dd($users);
    }

    public function index()
    {
        $users = User::select(['name', 'id'])
            ->take(5)
            ->get()
            ->shuffle()
            ->tap(function ($users) {
                info($users->first());
            })
            ->chunk(3);
    }

# Advanced Eloquent Relationships

## Polymorphic Relations Explained 

A polymorphic relationship allows the target model to belong to more than one type of model using a single association.

One To One (Polymorphic)

TABLES
migrations
photos
posts
products

| **Tables** |
|----------|
| migrations |
| photos |
| posts |
| products |


| **posts_photos** |
|----------|
| id |
| filename |
| post_id |
| timestamps |

| **products_photos** |
|----------|
| id  |
| filename |
| product_id |
| timestamps |

| **users_photos** |
|----------|
| id |
| filename |
| use_id |
| timestamps |

| **photos** |
|----------|
| id |
| filename |
| photoable_id |
| photoable_type |
| user_id |
| timestamps |

    Schema::create('photos', function (Blueprint $table) {
        $table->increments('id');
        $table->integer('imageable_id')->unsigned();
        $table->string('imageable_type');
        $table->string('filename');
        $table->timestamps();
    });

Photo model:

    class Photo extends model
    {
        protected $fillable = ['imageable_id', 'imageable_type', 'filename'];

        public function imageable()
        {
            return $this->morphTo();
        }
    }

Post model:

    class Post extends model
    {
        protected $fillable = ['title'];

        public function photos()
        {
            return $this->morphMany('App\Photo', 'imageable');
        }
    }

PostsController:

    public function store(Request $request)
    {
        $post = Post::create($request->only(['title']));
        $photos = explode(",", $request->get('photos')) ;
        foreach ($photos as $photo) {
            Photo::Create([
                'imageable_id' => $post->id,
                'imageable_type' => 'App\Post',
                'filename' => $photo
            ]);
        });
        return redirect()->route('posts.index');
    }

## Polymorphic Many-to-Many Relations 

One To Many (Polymorphic)

| **posts** |
|----------|
| id |
| title |

| **products** |
|----------|
| id |
| name |

| **photos** |
|----------|
| id |
| filename |

| **imageables**|
|---------|
| photo_id |
| imageable_id |
| imageable_type |

    Schema::create('imageables', function (Blueprint $table) {
        $table->unsignedInteger('photo_id');
        $table->foreign('photo_id')->references('id')->on('photos');
        $table->unsignedInteger('imageable_id');
        $table->string('imageable_type');
    });

Photo model:

    class Photo extends model
    {
        protected $fillable = ['filename'];

        public function products()
        {
            return $this->morphedByMany('App\Product', 'imageable');
        }

        public function posts()
        {
            return $this->morphedByMany('App\Post', 'imageable');
        }
    }

Product model:

    class Product extends model
    {
        protected $fillable = ['title'];

        public function photos()
        {
            return $this->morphedByMany('App\Photo', 'imageable');
        }
    }

Post model:

    class Post extends model
    {
        protected $fillable = ['title'];

        public function photos()
        {
            return $this->morphedByMany('App\Photo', 'imageable');
        }
    }

Imageable model:

    class Imageable extends model
    {
        public $timestamps = false;
        protected $fillable = ['photo_id', 'imageable_id', 'iamgeable_type'];
    }

PostController:

    public function store(Request $request)
    {
        $post = Post::create($request->only(['title']));
        $photos = explode(",", $request->get('photos')) ;
        foreach ($photos as $filename) {
            $photo = Photo::Create([
                'filename' => $filename
            ]);

            Imageable::create([
                'photo_id' => $photo->id
                'imageable_id' => $post->id,
                'imageable_type' => 'App\Post',
            ]);

        return redirect()->route('posts.index');
    }


## Advanced Pivot Tables in Many-to-Many 

    Schema::create('roles', function (Blueprint $table) {
        $table->increments('id');
        $table->string('name');
        $table->timestamps();
    });

    Schema::create('role_user', function (Blueprint $table) {
        $table->unsignedInteger('role_id');
        $table->foreign('role_id')->references('id')->on('roles');
        $table->unsignedInteger('user_id');
        $table->foreign('user_id')->references('id')->on('users');
        $table->boolen('approved')->default(0);
        $table->timestamps();
    });

    class User extends Authenticatable
    {
        use Notifiable;

        protected $fillable = [
            'name','email','password',
        ];

        protected $hidden = [
            'password','remember_token',
        ];

        public function roles()
        {
            return $this->belongsToMany(Role::class)->withTimestamps()->withPivot('approved');
        }

        public function approvedRoles()
        {
            return $this->belongsToMany(Role::class)->wherePivot('approved', 1);
        }
    }

`DatabaseSeeder`:

    public function run()
    {
        \App\Role::create(['name' => 'Administrator']);
        \App\Role::create(['name' => 'Editor']);
        \App\Role::create(['name' => 'Author']);

        $user = \App\User::Create([
            'name' => 'Administrator',
            'email' => admin@admin.com,
            'password' => bvrypt('password');
        ]);
        $user->roles()->attach(1, ['approved' => 1]);
        $user->roles()->attach(2);

        foreach($user->roles as $role) {
            //info($role->name . '(time '.$role->pivot->created_at', approved: '. $role->pivot->approved.')');
            info($role->name);
        }
    }

## HasManyThrough Relations 

    Schema::create('users', function (Blueprint $table) {
        $table->unsignedInteger('role_id');
        $table->foreign('role_id')->references('id')->on('roles');
        $table->string('name');
        $table->string('email')->unique();
        $table->timestamp('email_verified_at')->nullable();
        $table->string('password');
        $table->rememberToken();
        $table->timestamps();
    });

    Schema::create('roles', function (Blueprint $table) {
        $table->increments('id');
        $table->string('name');
        $table->timestamps();
    });

    Schema::create('posts', function (Blueprint $table) {
        $table->increments('id');
        $table->unsignedInteger('user_id');
        $table->foreign('user_id')->references('id')->on('users');
        $table->string('title');
        $table->text('post_text');
        $table->timestamps();
    });

User model:

    class User extends Authenticatable
    {
        use Notifiable;

        protected $fillable = [
            'name','email','password', 'role_id',
        ];

        protected $hidden = [
            'password','remember_token',
        ];

        public function role()
        {
            return $this->belongsTo(Role::class);
        }

        public function posts()
        {
            return $this->hasMany(Post::class);
        }
    }

Role model:

    class Role extends model
    {
        protected $fillable = ['name'];

        public function users()
        {
            return $this->hasMany(User::class);
        }

        public function posts()
        {
            return $this->hasManyThrough(Post::class, User::class);
        }
    }

Post model:

    class Post extends model
    {
        protected $fillable = ['user_id', 'title', 'post_text'];

        public function user()
        {
            return $this->belongsTo(User::class);
        }
    }

`DatabaseSeeder`:

    public function run()
    {
        \App\Role::create(['name' => 'Administrator']);
        \App\Role::create(['name' => 'Editor']);
        \App\Role::create(['name' => 'Author']);

        $user = \App\User::Create([
            'role_id' => 1,
            'name' => 'Administrator',
            'email' => admin@admin.com,
            'password' => bvrypt('password');
        ]);
        $user = \App\User::Create([
            'role_id' => 2,
            'name' => 'Editor',
            'email' => editor@editor.com,
            'password' => bvrypt('password');
        ]);
        $user = \App\User::Create([
            'role_id' => 3,
            'name' => 'Author',
            'email' => author@author.com,
            'password' => bvrypt('password');
        ]);

        for ($i=1; $i <= 10; $i++) {
            \App\Post::create([
                'user_id' => rand(1, 3),
                'title' => str_random(10),
                'post_text' => str_random(200),
            ]);
        }
    }

`HomeController`:

class HomeController extends Controller
{
    public function index()
    {
        $roles = Role::with('users.posts')->get();
        return view('home', compact('roles'));
    }
}

## Creating Records with Relationships 

    public function store(Request $request)
    {
        $author = Author::firstOrCreate(['name' => $request->author]);

        $titles = collect(explode(',', $request->titles))->map(function($record) {
            return ['title' => $record];
        })->toArray();

        $author->books()->createMany($titles);

        return redirect()->route('books.index');
    }

## Querying Records with Relationships

    class Book extends Model
    {
        protexted $fillable = ['author_id', 'title'];

        public function author()
        {
            return $this->belongsTo(Author::class);
        }

        public function ratings()
        {
            return $this->hasMany(Rating::class);
        }
    }

    public function index()
    {
        Author::whereHas('books', function($query){
            $query->where('title', 'like', '%b%');
        })->get()->dd();

        return view('books.index', compact('books'));
    }


# Eloquent Performance

## Laravel Debugbar: How to Measure Performance 

Installation:

    composer require barryvdh/laravel-debugbar --dev

Example:

    public function index()
    {
        $books = Book::with('author')
            ->where('title', 'like', '%a%')
            ->take(50)
            ->get();

        return view('books.index', compact('books'));
    }
    
Queries output in debugbar:

    select * from `books` where `title` like `%a%` limit 50 (1.46ms)

[Laravel Debugbar Github](https://github.com/barryvdh/laravel-debugbar)

## Performance Test: Eloquent vs Query Builder vs SQL

    public function test1()
    {
        $time_start = $this->microtime_float();

        $books = Book::with('author')
            ->where('title', 'like', '%a%')
            ->get();

        $time_end = $this->microtime_float();
        $time = $time_end - $time_start;

        return "Did nothing in $time seconds";
    }

    public function test2()
    {
        $time_start = $this->microtime_float();

        $books = \DB::table('books')
            ->join('authors', 'books.author_id', '=', 'authors.id')
            ->where('title', 'like', '%a%')
            ->get();

        $time_end = $this->microtime_float();
        $time = $time_end - $time_start;

        return "Did nothing in $time seconds";
    }

    public function test3()
    {
        $time_start = $this->microtime_float();

        $books = \DB::select("seelct * from books join authors on books.author_id = authors.id where title like %a%");

        $time_end = $this->microtime_float();
        $time = $time_end - $time_start;

        return "Did nothing in $time seconds";
    }

    private function microtime_float()
    {
        list($usec, $sec) = explode(" ", microtime());
        return ((float)$usec + (float)$sec);
    }

books/test1

    Did nothing in 0.40745592117310 seconds

books/test2
    
    Did nothing in 0.05786395072937 seconds

books/test3

    Did nothing in 0.07549003448486 seconds

## N+1 Problem and Eager Loading: Be Careful with Eloquent 

Controller:

    public function index()
    {
        $books = Book::where('title', 'like', '%a%')
            ->take(100)
            ->get();

        return view('books.index', compact('books'));
    }

view:

    @foreach ($books as $book)
        <tr>
            <td>{{ $book->title }}</td>
            <td>{{ $book->author->name }}</td>
        </tr>
    @endforeach

Laravel debugbar output:

    Queries 102 - 3.68s

Controller:

    public function index()
    {
        $books = Book::with('author')
            ->where('title', 'like', '%a%')
            ->take(100)
            ->get();

        return view('books.index', compact('books'));
    }

Laravel debugbar output:

    Queries 3 - 1.16s

[Laravel N+1 Query Detector](https://github.com/beyondcode/laravel-query-detector)

## Caching in Eloquent

    public function index()
    {
        $authors = Author::with('books')
        ->take(20)
        ->get();

        return view(books.index, compact('authors'));
    }

    public function getBooksCountAttribute()
    {
        return $this->books->count();
    }


Laravel Debugbar output:

    Queries 21 - 1.88s

You can use `Cache::remember` to caching the model for fifteen minutes. You can cache properties and associations on your models that are automatically updated (and the cache invalidated) when the model (or associated model) is updated.

Example:

    public function index()
    {
        $authors = Author->take(20)->get();

        return view(books.index, compact('authors'));
    }

    public function getBooksCountAttribute()
    {
        return Cache::remember('author-books-' . $this->id, 15, function(){
            return $this->books->count();
        });
    }

# Useful Packages to Extend Eloquent

## spatie/laravel-medialibrary: Associate files with Eloquent models 

Installation:

    composer require "spatie/laravel-medialibrary:^7.0.0"
    
You can publish the migration with:

    php artisan vendor:publish --provider="Spatie\MediaLibrary\MediaLibraryServiceProvider" --tag="migrations"

After the migration has been published you can create the media-table by running the migrations:

    php artisan migrate

This will create a media table:

    Schema::create('media', function (Blueprint $table) {
        $table->increments('id');
        $table->morphs('model');
        $table->string('collection_name');
        $table->string('name');
        $table->string('file_name');
        $table->string('mime_type')->nullable();
        $table->string('disk');
        $table->unsignedInteger('size');
        $table->json('manipulations');
        $table->json('custom_properties');
        $table->json('responsive_images');
        $table->unsignedInteger('order_column')->nullable();
        $table->nullableTimestamps();
    });

Create the symbolic link:

    php artisan storage:link

Create Book view:

    <form action="{{ route('books.store') }}" method="POST" enctype="multipart/form-data">
        @csrf

        Book title:
        <input type="text" class="form-control" name="title" />
        <br />

        Author:
        <select name="author_id" class="form-control">
            @foreach ($authors as $author)
                <option value="{{ $author->id }}">{{ $author->name }}</option>
            @endforeach
        </select>

        Cover image:
        <br />
        <input type="file" name="cover_image" />
        <br /><br />

        <input type="submit" value="Save book" />
    </form>

This should look like this:

<img width="1680" alt="Login" src="medialibrary.png">

Book model:

    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;
    use Spatie\MediaLibrary\HasMedia\HasMediaTrait;
    use Spatie\MediaLibrary\HasMedia\HasMedia;
    use Spatie\MediaLibrary\Models\Media;

    class Book extends Model implements HasMedia
    {
        use HasMediaTrait;

        protected $fillable = ['author_id', 'title'];

        public function author()
        {
            return $this->belongsTo(Author::class);
        }

        public function registerMediaConversions(Media $media = null)
        {
            $this->addMediaConversion('thumb')
                ->width(100)
                ->height(100);
        }
    }

BookController:

    <?php

    namespace App\Http\Controllers;

    use App\Book;
    use App\Author;
    use Illuminate\Http\Request;

    class BookController extends Controller
    {
        public function index()
        {
            $books = Book::with('author')->get();
            return view('books.index', compact('books'));
        }

        public function create()
        {
            $authors = Author::all();
            return view('books.create', compact('authors'));
        }

        public function store(Request $request)
        {
            $book = Book::create($request->all());

            if ($request->hasFile('cover_image')) {
                $book->addMediaFromRequest('cover_image')->toMediaCollection('cover_images');
            }

            return redirect()->route('books.index');
        }
    }


Index book view:

    <tbody>
        @foreach ($books as $book)
            <tr>
                <td>{{ $book->title }}</td>
                <td>{{ $book->author->name }}</td>
                <td>
                    <img src="{{ $book->getFirstMediaUrl('cover_images') }}">
                </td>
                </tr>
        @endforeach
    </tbody>

This should look like this:

<img width="1680" alt="Login" src="fullpath.png"> 

Index book view by adding the second parameter to `getFirstMediaUrl`:

    <tbody>
        @foreach ($books as $book)
            <tr>
                <td>{{ $book->title }}</td>
                <td>{{ $book->author->name }}</td>
                <td>
                    <img src="{{ $book->getFirstMediaUrl('cover_images', 'thumb') }}">
                </td>
                </tr>
        @endforeach
    </tbody>

This should look like this:

<img width="1680" alt="Login" src="thumb.png">   

[Associate files with Eloquent models - Github](https://github.com/spatie/laravel-medialibrary)

## dimsav/laravel-translatable: Package for Multilingual Models

    composer require dimsav/laravel-translatable

    php artisan make:model ArticleTranslation -m


    Schema::create('article_translations', function(Blueprint $table)
    {
        $table->increments('id');
        $table->integer('country_id')->unsigned();
        $table->string('name');
        $table->string('locale')->index();

        $table->unique(['country_id','locale']);
        $table->foreign('country_id')->references('id')->on('countries')->onDelete('cascade');
    });

 Configuration:

    php artisan vendor:publish --tag=translatable

Install laravel Collective:

    composer require "laravelcollective/html":"^5.4.0"

Article model:

    <?php

    namespace App;

    use Dimsav\Translatable\Translatable;
    use Illuminate\Database\Eloquent\Model;
    use Illuminate\Database\Eloquent\SoftDeletes;

    class Article extends Model
    {
        use SoftDeletes;
        use Translatable;

        protected $fillable = ['title', 'article_text'];
        public $translatedAttributes = ['title', 'article_text'];
    }

ArticleTranslation model:

    <?php

    namespace App;

    use Illuminate\Database\Eloquent\Model;

    class ArticleTranslation extends Model
    {
        public $timestamps = false;
        protected $fillable = ['title', 'article_text'];
    }

create view:

   {!! Form::open(['method' => 'POST', 'route' => ['admin.articles.store']]) !!}

    <div class="panel panel-default">
        <div class="panel-heading">
            @lang('global.app_create')
        </div>

        <div class="panel-body">
            <div class="row">
                <div class="col-xs-12 form-group">
                    {!! Form::label('en_title', trans('global.articles.title').' [EN]', ['class' => 'control-label']) !!}
                    {!! Form::text('en_title', old('en_title'), ['class' => 'form-control', 'placeholder' => '']) !!}
                    <p class="help-block"></p>
                    @if($errors->has('en_title'))
                        <p class="help-block">
                            {{ $erros->first('en_title') }}
                        </p>
                    @endif
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 form-group">
                    {!! Form::label('en_article_text', trans('global.articles.title').' [EN]', ['class' => 'control-label']) !!}
                    {!! Form::text('en_article_text', old('en_article_text'), ['class' => 'form-control', 'placeholder' => '']) !!}
                    <p class="help-block"></p>
                    @if($errors->has('en_article_text'))
                        <p class="help-block">
                            {{ $erros->first('en_article_text') }}
                        </p>
                    @endif
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 form-group">
                    {!! Form::label('es_title', trans('global.articles.title').' [ES]', ['class' => 'control-label']) !!}
                    {!! Form::text('es_title', old('es_title'), ['class' => 'form-control', 'placeholder' => '']) !!}
                    <p class="help-block"></p>
                    @if($errors->has('es_title'))
                        <p class="help-block">
                            {{ $erros->first('es_title') }}
                        </p>
                    @endif
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 form-group">
                    {!! Form::label('es_article_text', trans('global.articles.title').' [ES]', ['class' => 'control-label']) !!}
                    {!! Form::text('es_article_text', old('es_article_text'), ['class' => 'form-control', 'placeholder' => '']) !!}
                    <p class="help-block"></p>
                    @if($errors->has('es_article_text'))
                        <p class="help-block">
                            {{ $erros->first('es_article_text') }}
                        </p>
                    @endif
                </div>
            </div>

ArticlesController:

    public function store(StoreArticlesRequest $request)
    {
        if(! Gate::allows('article_create')){
            return abort(401);
        }
        Article::create(
            [
                'en' => [
                    'title' => $request->en_title,
                    'article_text' => $request->en_article_text
                ],
                'es' => [
                    'title' => $request->es_title,
                    'article_text' => $request->es_article_text
                ]
            ]
        );
        return redirect()->route('admin.articles.index');
    }


`app.php`:

    /*
    |--------------------------------------------------------------------------
    | Application Locale Configuration
    |--------------------------------------------------------------------------
    |
    | The application locale determines the default locale that will be used
    | by the translation service provider. You are free to set this value
    | to any of the locales which will be supported by the application.
    |
    */

    'locale' => 'en',

to translate any field we use the translate method:

    {{ $article->translate('es')->title }}

[A Laravel package for multilingual models](https://github.com/dimsav/laravel-translatable)
