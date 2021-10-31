# Design patterns | Singleton

Singleton consists in allow only a unique instance of a class

This is useful only in a very specific situations, such as write a log file. Probably you won't be interested in allow multiple instances writing simultaneusly in your log file (or yes, as it depends of the app structure)

To achieve this, you just need to make the constructor private

By this move, you won't be able to instance the class outside the class, so the first and unique instance allowed will be instanced inside the class

To don't create a second instance any time you call the class, you must check if a first instance already exists. If it does, then you return it. If it doesn't, then you create the first instance and return it.


```ts
class Singleton {
	private static instance: Singleton

	private constructor() { }

	public static getInstance(): Singleton {
		if (!Singleton.instance) {
			Singleton.instance = new Singleton()
		}
		return Singleton.instance
	}
}
```


## Problems: unit testing

The main problem with Singleton design pattern, is that it complicates the unit testing

Because we have a unique instance, we won't be able to use it in our test in a simple way, as we can't create more instances to test different use cases.

The most common workaround is allow 2 instances instead of 1: one to use in the program, and a second one to use in testing