# Events

## Listening

A Service can listen to events and it's very simple:

```php
use Archict\Brick\ListeningEvent;
use Archict\Brick\Service;

#[Service]
class MyService
{
    #[ListeningEvent]
    public function listenToSomeEvent(MyEvent $event): void
    {
    }
}
```

It just need a method with the attribute `ListeningEvent`. Archict will infer which event is listened by getting type of first parameter. Note that the method MUST have one and only one parameter, the event listened which is an object.

## Dispatching

Dispatching of Events is done by using `Archict\Core\Event\EventDispatcher::dispatch(object)`. `EventDispatcher` is a Service provided by `Archict/Core`, it can be retrieved from the dependency injection of another Service. The dispatcher will returns the object passed to the method modified by all the listeners. The calling order of listeners cannot be predicted, be vigilant on that.
