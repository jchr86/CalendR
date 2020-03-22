# CalendR

[![Build Status](https://travis-ci.org/yohang/CalendR.svg?branch=1.1)](https://travis-ci.org/yohang/CalendR)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/yohang/CalendR/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/yohang/CalendR/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/yohang/CalendR/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/yohang/CalendR/?branch=master)
[![SensioLabsInsight](https://insight.sensiolabs.com/projects/ac050bc0-c3b2-4d88-be63-059a0d968157/mini.png)](https://insight.sensiolabs.com/projects/ac050bc0-c3b2-4d88-be63-059a0d968157)

CalendR is an Object Oriented Calendar management library on top of PHP5.3+ Date objects.
You can use it to deal with all your needs about calendars and events.

Complete documentation
----------------------

Complete documentation is available [here](http://yohang.github.com/CalendR).

Installation
------------

CalendR is hosted on [packagist](http://packagist.org), you can install it with composer.

Open a command console, enter your project directory and execute:
```console
$ composer require jchr86/calendr
```

Applications that use Symfony Flex
----------------------------------

### Enable the Bundle.

Enable the bundle by adding it to the list of registered bundles
in the `config/bundles.php` file of your project:

```php
// config/bundles.php

return [
    // ...
    CalendR\Bridge\Symfony\Bundle\CalendRBundle::class => ['all' => true],
];
```

### Register an event provider.

```php
// src/Repository/EventRepository.php

namespace App\Repository;

use App\Entity\Event;
use CalendR\Bridge\Doctrine\ORM\EventRepository;
use CalendR\Event\Provider\ProviderInterface;
use Doctrine\Bundle\DoctrineBundle\Repository\ServiceEntityRepository;
use Doctrine\Common\Persistence\ManagerRegistry;
use Doctrine\ORM\Query\Expr;

class EventRepository extends ServiceEntityRepository implements ProviderInterface
{
    use EventRepository;

    public function __construct(ManagerRegistry $registry)
    {
        parent::__construct($registry, Event::class);
    }
}
```

```yaml
// config/services.yaml

services:
    App\Repository\EventRepository:
        tags:
            - { name: calendr.event_provider }
```


Contribute
----------

Calendar is open to contributions. Merging delays can vary depending to my free time, but always be welcome.

License
-------

CalendR is licensed under the MIT License - see the LICENSE file for details
