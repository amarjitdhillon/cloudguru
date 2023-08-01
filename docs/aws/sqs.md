# SQS

SQS will guarantee that a message is delivered at least once, but that message may be redelivered.

SQS queues only make an “attempt” to deliver messages in order (more or less a FIFO approach) but do not guarantee FIFO. If strict FIFO is needed, that option can be selected.

## SNS

SNS manages notifications and SQS manages messages. SNS is a push-based system while SQS is a pull-based system.