# TravelMate - Hotel Booking Sequence Diagram

This diagram describes the interaction between the user,
TravelMate System, and Bank during hotel booking and payment.

```mermaid
sequenceDiagram
    actor User as User
    participant TM as TravelMate System
    participant Bank as Bank
User->>TM: Select hotel and room
    User->>TM: Submit booking details
    TM->>TM: Validate details and check availability
alt Room unavailable
        TM-->>User: Room is unavailable
    else Room available
        TM-->>User: Show total price
        User->>TM: Confirm payment
        TM->>Bank: Send payment request
        Bank->>Bank: Process payment
alt Payment successful
            Bank-->>TM: Payment approved
            TM-->>User: Booking confirmed
        else Payment failed
            Bank-->>TM: Payment declined
            TM-->>User: Payment unsuccessful
        end
    end
