## Can I compare frames with hw-frames also on Nstreme links? 

The frames counts only those which contain actual data. In the case of Nstreme, only the ACK can be transmitted in a single frame, if there is no other data to send. These ACK frames will not be added to the frames count, but they will appear at hw-frames . If there is traffic on both directions at maximum speed (eg. there will be no only-ack frames), then you can't compare frames to hw-frames as in case of regular wireless links.
