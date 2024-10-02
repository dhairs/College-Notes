```c++

Semaphore players = -3;
Semaphore game = 0;
Semaphore collapses = -3;
Semaphore done = 0;

void players() {
	//get ready
	sema_up(&players);
	
	//wait for game
	sema_down(&game);
	
	// < play sport >
	sema_up(&collapses)

	sema_down(&done);
	// 
}
```