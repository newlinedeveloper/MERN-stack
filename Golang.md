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
