# Social-Networking-Platform
Mini Project 3 – Designing a DSI Social Network Database in Neo4j

## Database Design & Setup
**Nodes:**

1. User: individuals on the platform
- Properties: user_id (unique identifier), name (full name), username (unique username), graduation_year (year of graduation), email (email address), linkedin_profile (LinkedIn profile URL), interest (career interest: data science, data analytics, etc.), company_name (name of current employer), current_position (job title)

2. Post: content shared by users
- Properties: post_id (unique identifier), title (title of the post), body (content of the post), date (date of post creation), type (type of post: text, link, image, video, etc.)

3. Event: events that users can attend
- Properties: event_id (unique identifier), name (name of the event), description (details about the event), date (date of the event), location (venue of the event)

4. Comment: user comments on posts
- Properties: comment_id (unique identifier), text (content of the comment), date (date the comment was posted), seen_status (indicates if the comment has been read)

**Edges:**

1. FRIENDS_WITH (User ↔ User): Indicates a friendship relationship between two users
- Properties: since (date the friendship started)

2. CREATED (User → Post): Indicates which user created a specific post
- No additional properties

3. ATTENDING (User → Event): Shows that a user is going to or interested in an event
- Properties: rsvp_date (date the user confirmed attendance)

4. COMMENTED_ON (User → Comment → Post): Connects a user and their comment to a post
- Properties: date (date the comment was made)

5. FOLLOWING (User → User): Represents one user following another without mutual friendship
- Properties: since (date when the following started)

6. HOSTS (User → Event): Indicates which user is hosting a particular event
- Properties: date (date when the user announced hosting the event)

## Rationale
**Nodes:**
- User: The core entity of the platform, representing the social aspect (users will include students, alumni, professors, recruiters, etc.)
- Post: A medium for users to express thoughts, share information, and interact
- Event: Facilitates real-world interactions and community building
- Comment: Encourages discussion and engagement on posts or events

**Edges:**
- FRIENDS_WITH: Allows the platform to create a network graph of social connections
- CREATED: Establishes content ownership, critical for user engagement
- ATTENDING: Enables the platform to suggest events to users based on their network
- COMMENTED_ON: Connects user opinions and discussions to content
- FOLLOWING: Allows users to receive updates without mutual connections
- HOSTS: Identifies organizers of events, important for event credibility


## Potential benefits and challenges of the platform
**Benefits:**
- Enhanced Networking Opportunities: The FRIENDS_WITH and FOLLOWING relationships can facilitate professional networking by connecting individuals with similar interests or within the same industry. The platform can support the formation of professional communities (just like LinkedIn, but it could be better for only mututal connections to allow message or other functionalities)

- Event Engagement: The ATTENDING and HOSTS relationships enable the platform to promote events more effectively. Users can discover events that align with their interests and connect with event hosts

- Community Building and Interaction: Users can comment on posts (COMMENTED_ON), fostering discussion and community interaction (different platforms use different kind of comment, for Twitter, you can comment on comment, but this could be computationally costly?)

- Career and Personal Development: With properties like graduation_year, company_name, and current_position, the platform can facilitate mentorship and career development opportunities for recent graduates and students who are still at school

**Challenges:**
- Data Privacy and Security: With users' personal information, such as email and LinkedIn profiles, there's a need for robust data protection measures to prevent data breaches and unauthorized access

- Scalability: As the number of users and interactions grows, ensuring the platform scales effectively without a drop in performance can be challenging, especially with complex queries on a graph database (such as: Given two Users, identify if they are indirectly connected through a chain of friends and, if so, return the connecting path. For instance, can you find a relationship path where Alice is friends with someone (say, Bob), who in turn is friends with Charlie?)

- User Engagement: Keeping users engaged with relevant content and ensuring they contribute to posts and events can be challenging. The platform must have algorithms to ensure users see engaging content without overwhelming them (recommendation system & NLP).

- Spam and Content Moderation: With any user-generated content platform, there's a risk of spam or inappropriate content. Implementing effective moderation tools and algorithms to manage this is a significant challenge.

- Complexity of Graph Queries: Writing efficient Cypher queries can become complex, especially when dealing with multi-layered relationships. This complexity increases with the scale of data and can impact performance.

## Gen AI
I created a GPT that helped me create some fake data. After I gave the schema, template commands for inserting data, & other instructions, it helped me create nodes data and edges data.
https://chat.openai.com/g/g-4RFCdK5Qr-neo4j-data-generator

