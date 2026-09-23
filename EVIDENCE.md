# Booking Lab Evidence Record

**Name:** [Aleksei Petukhov]
**Student ID:** [6280775]
**Repository:** [https://github.com/emb0dormo/iccs471-booking-lab-Aleksei-Pet/tree/main]

## Goal
[What booking behavior were you asked to change?]
 - I was asked to modify how every same room booking overlap raises ValueError and is not stored properly. Had to preserve existing validation which is gonna allow adjacent bookings and overlapping times in different rooms.

## Constraints / Out of Scope
[Which code and test files could you change? What behavior had to remain intact?]
 - Only booking_app/booking.py and test/test_booking.py were allowed to be edited

## Key Decision and Agent Claim
[Describe one part of Copilot's plan or implementation you checked and deliberately accepted, revised, or rejected. Why? If you made no correction, explain a choice you consciously accepted.]
 - Copilot's plan decided to prevent same-room booking overlaps suggested because this change adds a room overlap guard in the booking service while preserving the current validation. Since the service should reject any new booking that overlaps with existing one, so it should raive ValueError and leave the list unchanged. Therefore adjacent bookings remain valid and overlapping bookings in different rooms remain valid. He/It suggested to ensure the overlap rejection happens before storing a booking so invalid attempts are never added to the list which preserved the existing validation behavior.

[State one concrete claim Copilot made about the repository or its work. What file, code, or result did you inspect to check it? Was the claim accurate?]

 answer from copilot -> "Extend test_booking.py with a regression test that creates a same-room overlap and asserts ValueError while verifying the stored list remains unchanged." I checked the test cases he provided and agreed with them. for example test case "test_rejects_same_room_overlap_without_storing" works good and checks the room and does not store if it's equal

## Verification: Claim → Evidence
- **Claim:** [What specific behavior did you want to establish?]
- **Command or test I ran:** [Give the actual command or test.]
- **Actual result:** [What happened, including a failure and subsequent correction if relevant?]
- **What this supports:** [What does this result give you reason to believe?]

 1. Claim: I wanted to change create_booking so that proposed booking that overlaps an existing booking in the same room raises ValueError and rejection must not be stored.
 2. Test I ran "uv run python -m unittest discover -s tests -v" 
 results:
    test_allows_adjacent_bookings_in_same_room (test_booking.BookingServiceTests.test_allows_adjacent_bookings_in_same_room) ... ok
test_allows_overlapping_times_in_different_rooms (test_booking.BookingServiceTests.test_allows_overlapping_times_in_different_rooms) ... ok
test_bookings_remain_in_creation_order (test_booking.BookingServiceTests.test_bookings_remain_in_creation_order) ... ok
test_create_and_list_booking (test_booking.BookingServiceTests.test_create_and_list_booking) ... ok
test_rejects_blank_room_or_guest (test_booking.BookingServiceTests.test_rejects_blank_room_or_guest) ... ok
test_rejects_invalid_time_range (test_booking.BookingServiceTests.test_rejects_invalid_time_range) ... ok
test_rejects_same_room_overlap_without_storing (test_booking.BookingServiceTests.test_rejects_same_room_overlap_without_storing) ... ok

It succeded and test had ValueError and it works well.

I ran : 
(iccs471-booking-starter) PS C:\Users\acer\booking-lab> uv run python demo.py
First booking in room A: accepted
Overlapping booking in room A: rejected (booking overlaps an existing booking in the same room)
Adjacent booking in room A: accepted
Overlapping time in room B: accepted
Stored bookings: 3

Which shows that it did the task and met the requirements and it shows to me that it worked well and made me believe it.

## Manual Validation
[What happened when you personally ran demo.py? What did it show beyond the original four baseline tests?]

(iccs471-booking-starter) PS C:\Users\acer\booking-lab> uv run python demo.py
First booking in room A: accepted
Overlapping booking in room A: rejected (booking overlaps an existing booking in the same room)
Adjacent booking in room A: accepted
Overlapping time in room B: accepted
Stored bookings: 3

it shows that the overlapping did not happen in room A, rejected booking was not stored. it is possible to book to other rooms (adjecent for example)

## Remaining Uncertainty
[Name one plausible booking case, limitation, or risk that your checks did not fully establish.]
- since it's a small task I think I did not cover every edge-case. what if user tried to book millions times? How would it behave. if two and more people would like to book at the same time. I have not provided every possible idea(edge-case)