File Driver
===========

File driver uses files to store queue data.

Configuration example:

```php
return [
    'bootstrap' => [
        'queue', // The component registers own console commands
    ],
    'components' => [
        'queue' => [
            'class' => \zhuravljov\yii\queue\file\Queue::class,
            'path' => '@runtime/queue',
        ],
    ],
];
```

Console
-------

Console command is used to execute tasks.

```bash
yii queue/run
```

`run` command obtains and executes tasks in a loop until queue is empty. Works well with cron.

```bash
yii queue/listen [delay]
```

`listen` command launches a daemon which infinitely queries the queue. If there are new tasks they're immediately
obtained and executed. `delay` is time in seconds to wait between querying a queue next time.
This method is most effificient when command is properly daemonized via supervisor such as
`supervisord`.

`run` and `listen` commands have options:

- `--verbose`, `-v`: print executing statuses into console.
- `--isolate`: verbose mode of a job execute. If enabled, execute result of each job will be printed.
- `--color`: highlighting for verbose mode.

```bash
yii queue/info
```

`info` command prints out information about queue status.
