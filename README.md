## Laravel Core
The Laravel package to provide core functionalities of [Laravel dashboard](https://laravue.dev)

## Installations

[Laravue](https://github.com/tuandm/laravue) is to provide an enterprise solution for an admin dashboard, therefore it's highly recommended to start a project with it. The following instructions are for intergrating core features of Laravue to existing Laravel project or to experiement with it.


#### Install laravue-core package

```
composer require tuandm/laravue-core
```
#### Setup environment for Laravue (API endpoint and JWT secret)

##### Setup Laravue
```
php artisan laravue:setup
```

##### Open `config/auth.php` and modify as below

```
    # Change default auth guard to api
    'defaults' => [
        'guard' => 'api',
    ],
    ...
    # Use JWT driver for api guard
    'guards' => [
    ....
    'api' => [
        'driver' => 'jwt',
    ....
    
    # Use Laravue User model to authenticate
    'providers' => [
        'users' => [
            'driver' => 'eloquent',
            'model' => Tuandm\Laravue\User::class,
        ],
``` 
Please reference to [auth.php sample](https://github.com/tuandm/laravue-core/tree/master/src/config/auth.php.sample)

#### Database
Laravue core requires `users.role` field, consider to run migration and data seeder (for sample data if necessary

```
php artisan migrate
php artisan db:seed --class=Tuandm\\Laravue\\Database\\Seeds\\DatabaseSeeder
```

#### Publish Laravue packages

```
php artisan vendor:publish --provider="Tuandm\Laravue\ServiceProvider" --tag="laravue-core"
php artisan vendor:publish --provider="Tuandm\Laravue\ServiceProvider" --tag="laravue-asset"
```

#### Add NPM dependencies
```
npm add babel-plugin-syntax-dynamic-import babel-plugin-syntax-jsx babel-plugin-transform-vue-jsx eslint eslint-loader eslint-plugin-vue laravel-mix-eslint vue-template-compiler svg-sprite-loader --save-dev

npm add element-ui js-cookie normalize.css nprogress vuex vue-count-to vue-i18n vue-router 

npm install # To make sure everything is set
```

Please check [package.json sample](https://github.com/tuandm/laravue-core/tree/master/package.json.sample)

#### Webpack.mix.js configuration
We need to modify the webpack.mix.js to work with Laravue package, please reference to [webpack.mix.js sample](https://github.com/tuandm/laravue-core/tree/master/webpack.mix.js.sample)

#### Babel
Laravue requires babel to build the packages. Usually, `.babelrc` will be generated with [laravue:setup command](#setup-laravue). Please manual add required plugins to `.babelrc` file if your project already uses it. Sample `.babelrc` can be found [here](https://github.com/tuandm/laravue-core/tree/master/.babelrc.sample)

#### Start development

```
npm run dev # or npm run watch
```

#### Build production

```
npm run production
```
