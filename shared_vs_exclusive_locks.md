# Shared Lock:
## Purpose: Shared locks are used when a transaction wants to read a resource without modifying it, and it allows other transactions to acquire shared locks on the same resource simultaneously.
## Concurrency: Multiple transactions can hold shared locks on the same resource simultaneously.
## Example Scenario:
// Laravel example using Eloquent ORM

    DB::beginTransaction();
    try {
        $article = Article::find(1);

        // Acquiring a shared lock on the article record
        $article->lockForShare()->get();
    
        // Perform read operations on the article
    
        DB::commit();
    } catch (\Exception $e) {
        DB::rollback();
        // Handle the exception
    }
------------

# Exclusive Lock:
## Purpose: Exclusive locks are used when a transaction intends to modify a resource, and it ensures that no other transactions can acquire shared or exclusive locks on the same resource until the lock is released.
## Concurrency: Only one transaction can hold an exclusive lock on a resource at a time.
## Example Scenario:
// Laravel example using Eloquent ORM

    DB::beginTransaction();
    try {
        $article = Article::find(1);
    
        // Acquiring an exclusive lock on the article record
        $article->lockForUpdate()->get();
    
        // Perform write operations on the article
    
        DB::commit();
    } catch (\Exception $e) {
        DB::rollback();
        // Handle the exception
    }
