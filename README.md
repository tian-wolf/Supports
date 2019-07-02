<h1 align="center">Supports</h1>

handle with array/config/logger etc.

## About log

### Register

#### Method 1

A application logger can extends `Tlwl\Supports\Log` and modify `createLogger` method, the method must return instance of `Monolog\Logger`.

```PHP
use Tlwl\Supports\Logger;
use Monolog\Logger;

class ApplicationLogger extends Logger
{
    /**
     * Make a default log instance.
     *
     * @author tlwl <tian_wolf@sina.com>
     *
     * @return Logger
     */
    public static function createLogger()
    {
        $handler = new StreamHandler('./log.log');
        $handler->setFormatter(new LineFormatter("%datetime% > %level_name% > %message% %context% %extra%\n\n"));

        $logger = new Logger('tlwl.private_number');
        $logger->pushHandler($handler);

        return $logger;
    }
}
```

#### Method 2

Or, just init the log service with:

```PHP
use Tlwl\Supports\Logger;

protected function registerLog()
{
    $logger = Logger::createLogger($file, $identify, $level);

    Logger::setLogger($logger);
}
```

### Usage

After registerLog, you can use Log service:

```PHP
use Tlwl\Supports\Logger;

Logger::debug('test', ['test log']);
```

## LICENSE 
[MIT](https://github.com/tian-wolf/supports/blob/master/LICENSE)
