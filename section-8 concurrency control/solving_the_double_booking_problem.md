# Solve Double Booking 
- To prevent two transactions from booking the same record at the same time in a MySQL database using Laravel
- you can use a combination of database transactions and proper locking mechanisms.
- Laravel provides the **lockForUpdate()** method to acquire a **"write lock"** on a database record, preventing other transactions from modifying it until the lock is released.

# Example

    public function makeBooking($userId, $resourceId, $startTime, $endTime)
    {
        DB::beginTransaction();
        try {
            // Find the record and lock it for update
            $booking = Booking::where('resource_id', $resourceId)
                ->where('start_time', $startTime)
                ->where('end_time', $endTime)
                ->lockForUpdate()
                ->first();
    
            // Check if the record exists
            if (!$booking) {
                // Handle the case where the record does not exist
                return response()->json(['error' => 'Record not found'], 404);
            }
    
            // Check if the record is already booked
            if ($booking->user_id !== null) {
                // Handle the case where the record is already booked
                return response()->json(['error' => 'Record already booked'], 400);
            }
    
            // Update the booking with the user ID to mark it as booked
            $booking->update(['user_id' => $userId]);
    
            // Commit the transaction
            DB::commit();
    
            return response()->json(['message' => 'Booking successful'], 200);
        } catch (\Exception $e) {
            // Rollback the transaction in case of an exception
            DB::rollback();
    
            // Handle the exception (log it, return an error response, etc.)
            return response()->json(['error' => 'Booking failed'], 500);
        }
    }

