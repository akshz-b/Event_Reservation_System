# Reservation System Simulation

## Overview

This program simulates a reservation system for events using multi-threading in C++. It models a scenario where multiple worker threads perform operations like inquiring about available seats, booking tickets, and canceling bookings for a number of events happening in an auditorium. The system is designed to handle concurrent access to shared resources such as available seats for events and a shared table to manage active queries.

## Features

- **Concurrent Query Handling:** The system supports up to 5 concurrent active queries at a time.
- **Multi-threading:** 20 worker threads simulate real-world scenarios where multiple users interact with the system concurrently.
- **Thread Safety:** Mutex locks and condition variables are used to ensure thread safety while accessing shared resources.
- **Random Query Execution:** Each worker thread randomly decides whether to inquire, book, or cancel tickets for an event.

## System Components

### Constants

- **`numOfEvents`:** Total number of events.
- **`capacityOfAuditorium`:** Maximum capacity of the auditorium.
- **`numOfWorkerThreads`:** Number of worker threads simulating users.
- **`maxActiveQueries`:** Maximum number of active queries allowed simultaneously.
- **`runningTime`:** Duration for which the simulation runs.
- **`minTickets` & `maxTickets`:** Minimum and maximum number of tickets that can be booked in a single transaction.

### Data Structures

- **`queryInfo`:** A struct that holds information about a query such as event ID, query type (inquire, book, cancel), and the thread ID that initiated the query.
- **`sharedTable`:** An array of `queryInfo` structures that holds the active queries being processed.
- **`availableSeats`:** A vector that tracks the number of available seats for each event.

### Mutex and Condition Variables

- **`tableMutex`:** Protects access to the `sharedTable`.
- **`seatMutex`:** Protects access to the `availableSeats`.
- **`tableCondition`:** A condition variable to manage access to the `sharedTable`.

### Functions

- **`workerThread`:** The function executed by each worker thread. It performs random queries (inquire, book, cancel) on events.
- **`getRandomNumberInRange`:** Generates a random number within a specified range.
- **`inquireEvent`:** Handles inquiries about seat availability for a specified event.
- **`bookEvent`:** Books a specified number of seats for an event if available.
- **`cancelEvent`:** Cancels a specified number of previously booked seats for an event.
- **`canRead`:** Checks if the event details can be read by a thread.
- **`canWrite`:** Checks if the event details can be updated by a thread.
- **`findBlankEntry`:** Finds a blank entry in the `sharedTable` to add a new query.

## How to Run the Program

1. **Compile the Program:**
   ```bash
   g++ -pthread -o reservation_system Event_Reservation_System.cpp
   ```

2. **Run the Program:**
   ```bash
   ./reservation_system
   ```

3. **Output:**
   The program will run for a specified duration (`runningTime`), during which worker threads will perform random queries. After the simulation ends, the program will print the final reservation status of all events, showing the percentage of seats booked and the number of seats left for each event.

## Notes

- The program uses `pthread` for multi-threading, so ensure that your environment supports `pthread`.
- The random number generation is seeded with the thread ID to ensure variability in queries.
- The program demonstrates basic concepts of thread synchronization using mutexes and condition variables.