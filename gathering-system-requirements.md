# Gathering System Requirements in System Design Interviews

System design interviews are intentionally vague. The interviewer will not give you a clear problem statement. Instead, they will ask you to design a system that can handle a certain load or a certain set of requirements. It is your job to ask the right questions to gather the requirements and constraints of the system.

They might ask you to design "Youtube". You need to ask questions like:

- What is the expected number of videos uploaded per day?
- What is the expected number of videos watched per day?
- What is the expected number of concurrent users?
- What is the expected number of comments per video?
- What is the expected number of likes per video?
- What part of Youtube are we designing? The video upload part, the video serving part, the comment serving part, etc.

The interviewer will not give you a clear answer to these questions. They will give you a range. For example, they might say "The number of videos uploaded per day can range from 1000 to 1000000". It is your job to design a system that can handle the upper limit of this range.

The scale may not have to do with users, but it can to do with the data itself, like the number of videos, the number of comments, the number of likes, etc.

## System characteristics

You also wanna ask about the characteristics of the system such as latency, throughput, consistency, availability, durability, etc.

If asked to design Youtube, you might ask:

- What is the expected latency for video upload?
- What is the expected latency for video serving?
- What is the expected throughput for video upload?
- What is the expected throughput for video serving?
- What is the expected consistency level for video serving?
- What is the expected availability for video serving?
