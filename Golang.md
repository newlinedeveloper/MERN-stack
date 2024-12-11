#### Concurrency with multiple queue examples

```
package main

import (
	"fmt"
	"sync"
)

// Worker function using select to manage multiple channels
func displayOddOrEven(id int, evenQueue, oddQueue <-chan int, wg *sync.WaitGroup) {
	defer wg.Done()
	for {
		select {
		case job, ok := <-evenQueue:
			if !ok { // Channel closed
				evenQueue = nil // Disable this case
			} else {
				fmt.Printf("Even no: %d, worker id: %d\n", job, id)
			}
		case job, ok := <-oddQueue:
			if !ok { // Channel closed
				oddQueue = nil // Disable this case
			} else {
				fmt.Printf("Odd no: %d, worker id: %d\n", job, id)
			}
		}
		// Break when all channels are nil
		if evenQueue == nil && oddQueue == nil {
			break
		}
	}
}

func main() {
	var wg sync.WaitGroup
	jobCount := 10
	workerCount := 3
	oddQueue := make(chan int, jobCount)
	evenQueue := make(chan int, jobCount)

	// Start workers
	for i := 1; i <= workerCount; i++ {
		wg.Add(1)
		go displayOddOrEven(i, evenQueue, oddQueue, &wg)
	}

	// Distribute jobs
	for j := 1; j <= jobCount; j++ {
		if j%2 == 0 {
			evenQueue <- j
		} else {
			oddQueue <- j
		}
	}

	// Close channels to signal completion
	close(oddQueue)
	close(evenQueue)

	// Wait for all workers to finish
	wg.Wait()
	fmt.Println("Queue process completed")
}


```

#### **Q1: What are some commonly used design patterns in Go?**

- **Singleton Pattern**:
  - Ensures a single instance of a resource is created and provides global access to it.
  - Example:
    ```go
    package main

    import "sync"

    type Singleton struct{}

    var instance *Singleton
    var once sync.Once

    func GetInstance() *Singleton {
        once.Do(func() {
            instance = &Singleton{}
        })
        return instance
    }

    func main() {
        s1 := GetInstance()
        s2 := GetInstance()
        println(s1 == s2) // Output: true
    }
    ```

- **Factory Pattern**:
  - Provides a way to create objects without specifying the exact class.
  - Example:
    ```go
    package main

    import "fmt"

    type Shape interface {
        Draw()
    }

    type Circle struct{}

    func (c Circle) Draw() {
        fmt.Println("Drawing Circle")
    }

    type Rectangle struct{}

    func (r Rectangle) Draw() {
        fmt.Println("Drawing Rectangle")
    }

    func ShapeFactory(shapeType string) Shape {
        switch shapeType {
        case "circle":
            return Circle{}
        case "rectangle":
            return Rectangle{}
        default:
            return nil
        }
    }

    func main() {
        shape := ShapeFactory("circle")
        shape.Draw() // Output: Drawing Circle
    }
    ```

---

#### **Q2: How is the Observer pattern implemented in Go?**

- **Observer Pattern**:
  - Allows an object (subject) to notify multiple observers of changes to its state.

- **Implementation**:
  ```go
  package main

  import "fmt"

  type Observer interface {
      Update(message string)
  }

  type Subject struct {
      observers []Observer
  }

  func (s *Subject) Attach(observer Observer) {
      s.observers = append(s.observers, observer)
  }

  func (s *Subject) Notify(message string) {
      for _, observer := range s.observers {
          observer.Update(message)
      }
  }

  type ConcreteObserver struct {
      ID int
  }

  func (c *ConcreteObserver) Update(message string) {
      fmt.Printf("Observer %d received: %s\n", c.ID, message)
  }

  func main() {
      subject := &Subject{}

      observer1 := &ConcreteObserver{ID: 1}
      observer2 := &ConcreteObserver{ID: 2}

      subject.Attach(observer1)
      subject.Attach(observer2)

      subject.Notify("Update available!") // Both observers receive the message
  }
  ```

---

#### **Q3: Can you explain the Decorator pattern with an example in Go?**

- **Decorator Pattern**:
  - Allows behavior to be added to an object dynamically.

- **Implementation**:
  ```go
  package main

  import "fmt"

  type Notifier interface {
      Send(message string)
  }

  type EmailNotifier struct{}

  func (e EmailNotifier) Send(message string) {
      fmt.Printf("Sending email: %s\n", message)
  }

  type SMSDecorator struct {
      Notifier Notifier
  }

  func (s SMSDecorator) Send(message string) {
      s.Notifier.Send(message)
      fmt.Printf("Sending SMS: %s\n", message)
  }

  func main() {
      email := EmailNotifier{}
      sms := SMSDecorator{Notifier: email}

      sms.Send("Hello, Go!") // Both email and SMS are sent
  }
  ```

---

#### **Q4: How is the Strategy pattern implemented in Go?**

- **Strategy Pattern**:
  - Allows selecting an algorithm's behavior at runtime.

- **Implementation**:
  ```go
  package main

  import "fmt"

  type PaymentStrategy interface {
      Pay(amount int)
  }

  type CreditCard struct{}

  func (c CreditCard) Pay(amount int) {
      fmt.Printf("Paid %d using Credit Card\n", amount)
  }

  type PayPal struct{}

  func (p PayPal) Pay(amount int) {
      fmt.Printf("Paid %d using PayPal\n", amount)
  }

  type PaymentProcessor struct {
      Strategy PaymentStrategy
  }

  func (pp PaymentProcessor) ProcessPayment(amount int) {
      pp.Strategy.Pay(amount)
  }

  func main() {
      processor := PaymentProcessor{Strategy: CreditCard{}}
      processor.ProcessPayment(100)

      processor.Strategy = PayPal{}
      processor.ProcessPayment(200)
  }
  ```

---

#### **Q5: How do you implement the Builder pattern in Go?**

- **Builder Pattern**:
  - Separates the construction of a complex object from its representation.

- **Implementation**:
  ```go
  package main

  import "fmt"

  type Car struct {
      Brand  string
      Color  string
      Engine string
  }

  type CarBuilder struct {
      car Car
  }

  func (b *CarBuilder) SetBrand(brand string) *CarBuilder {
      b.car.Brand = brand
      return b
  }

  func (b *CarBuilder) SetColor(color string) *CarBuilder {
      b.car.Color = color
      return b
  }

  func (b *CarBuilder) SetEngine(engine string) *CarBuilder {
      b.car.Engine = engine
      return b
  }

  func (b *CarBuilder) Build() Car {
      return b.car
  }

  func main() {
      car := CarBuilder{}.
          SetBrand("Tesla").
          SetColor("Red").
          SetEngine("Electric").
          Build()

      fmt.Printf("Car: %+v\n", car)
  }
  ```

---

