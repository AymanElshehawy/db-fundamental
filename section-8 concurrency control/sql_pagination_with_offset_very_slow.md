# SQL Pagination Offset Very Slow
- Using `OFFSET` in pagination can be slow, especially with large datasets, due to the way it operates. When you use OFFSET
- the database engine has to physically skip a certain number of rows before returning the desired page of results. 
- This process can become increasingly inefficient as the offset value grows, and the performance impact is more noticeable with larger datasets. 
- Here are a few reasons why using `OFFSET` can be slow:

1. **Full Scans**:
- When you use `OFFSET`, the database engine might need to scan through and discard a large number of rows before reaching the offset point. This operation becomes more time-consuming as the offset increases.
- 
2. **Resource Consumption:**
- The database engine needs to perform extra work to skip rows, which involves additional I/O operations and processing time. This can result in increased resource consumption, leading to slower query performance.
- 
3. **Inefficient Index Usage:** 
- In some cases, if your query involves ordering and filtering, using `OFFSET` may prevent the database engine from efficiently using indexes, further impacting performance.

4. **Data Movement:** 
- Databases typically store rows in pages or blocks on disk. When using `OFFSET`, the database may need to fetch and discard entire pages of data, leading to unnecessary data movement and increased I/O operations.

## Laravel Example:-
- In Laravel, you can use the Eloquent ORM to achieve keyset pagination. Assuming you have a model named YourModel and you want to paginate based on the id column, here's how you can implement keyset pagination:

        public function index($lastSeenId = null, $direction = 'next')
        {
            $pageSize = 10;
    
            // Query based on the direction (next or previous)
            $query = YourModel::orderBy('id', ($direction === 'next') ? 'ASC' : 'DESC');
    
            // If lastSeenId is provided, add a where clause to the query
            if ($lastSeenId) {
                $operator = ($direction === 'next') ? '>' : '<';
                $query->where('id', $operator, $lastSeenId);
            }
    
            // Fetch the records
            $results = $query->limit($pageSize)->get();
    
            // Pass the results, lastSeenId, and direction to the view
            return view('your-view', [
                'results' => $results,
                'lastSeenId' => optional($results->last())->id, // Get the last ID from the results
                'direction' => $direction,
            ]);
        }