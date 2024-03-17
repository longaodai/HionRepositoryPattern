# LongAoDai Repository Pattern

This package provides a base repository implementation following the repository design pattern in PHP.

## Installation

You can install this package via Composer. Run the following command in your terminal:
```bash
composer require longaodai/hion-repository-pattern
```

## Usage
To use the base repository in your project, you need to create repository classes that extend the BaseRepository class provided by this package.

Here's an example of how to create a repository class:
```php
use LongAoDai\Repositories\BaseRepository;

class UserRepository extends BaseRepository
{
    /**
     * Specify the model class name.
     *
     * @return mixed
     */
    public function model()
    {
        return User::class;
    }
}

public function getList($data = null, $options = null): mixed
{
    $this->method('select', [
        'name', 'email'
    ]);

    return parent::getList($data, $options);
}

protected function filter($params): UserRepository
{
    if ($params->get('name')) {
        $this->method('where', 'name', 'like', '%' . $params->get('name') . '%');
    }

    if ($params->get('id')) {
        $this->method('where', 'id', $params->get('id'));
    }

    return parent::filter($params);
}

protected function mark($params): UserRepository
{
    if ($params->option('id')) {
        $this->method('where', 'id', $params->option('id'));
    }

    return parent::mark($params);
}
```
You can then use methods provided by the BaseRepository class such as all(), find(), create(), update(), and delete() in your repository classes.