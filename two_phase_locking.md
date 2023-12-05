# Two-Phase Locking (2PL) 
- is a concurrency control mechanism used in database systems to ensure serializability and avoid certain types of anomalies such as lost updates and uncommitted data. It consists of two phases: the growing phase and the shrinking phase.

Here's an explanation of Two-Phase Locking along with a simple Laravel example:

# Two-Phase Locking (2PL):

## Growing Phase:
- During the growing phase, transactions can acquire locks but cannot release any locks.
Once a transaction releases its first lock, it enters the shrinking phase.

## Shrinking Phase:
- In the shrinking phase, transactions can release locks but cannot acquire any new locks.
Once a transaction releases all its locks, it is considered to be completed.

## Laravel Example:
- Let's consider a scenario where we have a simple banking application using Laravel's Eloquent ORM to update user account balances.
## Transaction 1

    DB::beginTransaction();
    try {
        $user1 = User::find(1);
        $user1->update(['balance' => $user1->balance - 100]);
    
        // Acquire more locks or perform other operations
    
        $user2 = User::find(2);
        $user2->update(['balance' => $user2->balance + 100]);
    
        DB::commit();
    } catch (\Exception $e) {
        DB::rollback();
        // Handle the exception
    }

## Transaction 2

    DB::beginTransaction();
    try {
        $user2 = User::find(2);
        $user2->update(['balance' => $user2->balance - 50]);
    
        // Acquire more locks or perform other operations
    
        $user1 = User::find(1);
        $user1->update(['balance' => $user1->balance + 50]);
    
        DB::commit();
    } catch (\Exception $e) {
        DB::rollback();
        // Handle the exception
    }

In this example, we're using Laravel's transactions to represent two transactions, each updating the balance of two users. The Two-Phase Locking protocol is implicitly applied because Laravel's transactions automatically acquire locks when needed and release them upon successful commit.

## Growing Phase:
- In each transaction, locks are acquired during the course of execution (e.g., updating User 1 and User 2 balances).

## Shrinking Phase:
- After performing the required operations, locks are automatically released when the transaction is committed or rolled back.

## **Laravel's Eloquent ORM handles the details of acquiring and releasing locks based on the operations performed within a transaction. The use of Laravel's transactions ensures that transactions adhere to the Two-Phase Locking protocol, helping to prevent issues like lost updates and uncommitted data.**
