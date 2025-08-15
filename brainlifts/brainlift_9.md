Product BrainLift - Jive

- Owners
  - Ben New (TPM) [ben.new@devfactory.com](mailto:ben.new@devfactory.com)
- Purpose
  - To describe the **[Jive employee engagement platform](https://www.jivesoftware.com/)**, the problems it solves for customers, and how it solves those problems.
  - This is not a technically focused document, it is more focused on the customers and users, and how Jive is used by and useful to them. Technical details are included but not the primary focus.
  - This BrainLift is about the Jive core product, it does not discuss customer-specific details. For example, it talks about the customization capabilities in the product, but does not discuss how any specific customer uses those capabilities.

# DOK4 - Extended Thinking (SPOV for value creation)

- SPOV: Forced customer upgrades are essential; the current approach is actively endangering the security of the customer data and users.
- SPOV: Addressing technical debt is essential; ignoring it will lead to complete atrophy of the product.
- SPOV: We need to resolve the FUD around generative AI, because it is the most valuable tool we can use today.
  - Data sovereignty should not be a blocker; can be easily solved with customer keys or local LLMs. We should work with customers to clarify that and then focus on use-cases.
- SPOV: We should make the web UI fully responsive so it works well on mobile and ditch the native mobile application.

# DOK3 - Strategic Thinking (Analysis and Insights)

- Insight: Jive Unity provides the basis for improved pace on product development ([source](https://docs.google.com/document/d/1pPVbp5VNy-cUfAGic4DAtXxYjqNGDJSCsPZpez6RdGI/edit?tab=t.0#bookmark=id.tiyw2zbqgaad)):
  - Jive Cloud customers will be using an upgraded, secure product (the original request that led to the Jive Unity strategy was to upgrade several core components of Jive Cloud, when similar upgrades had already been done to Jive HOP).
  - The Jive Cloud codebase can be archived, greatly reducing maintenance and operational overhead.
  - Several services, which exist solely or almost solely for Jive Cloud, can be shut down, reducing AWS costs.
  - The resulting combined Jive will have the superset of all features currently in Jive HOP and Jive Cloud.
  - Any new features will naturally be available to all customers.
  - All future upgrades will be available to all customers. This is especially relevant given the impending need to upgrade Java and Spring.
- Insight: The majority of Jive customers are resistant to change.
  - Opposition to enabling Jive Copilot, an LLM-based assistant, because of FUD about generative AI.
  - Slow to upgrade, some customers still using very old versions of Jive, 5+ years old, despite having components and libraries severely beyond their EOL.
  - Even SaaS customers are resistant to having us apply managed upgrades, and legacy Hosted HOP customers are still using very old versions.
- Insight: There is a major disconnect between the importance of Jive instances to be secure (as evidenced by the fact that customers report security vulnerabilities), and the fact that most customers are reluctant to upgrade.
  - Despite recent upgrades, Jive still requires further upgrades to core components and libraries.
  - However, due to customer reluctance to upgrade, many customers have not yet adopted the upgrades already made.
  - The wider the gap between the version a customer is using and the current version, the greater the risk of things breaking when an upgrade eventually happens, and the more difficult it is to find the root cause.
  - In relation the legacy Hosted HOP customers, this leaves us in a difficult position, because we are running vulnerable software for customers, despite having already fixed those vulnerabilities in later versions of the software (!)
- Insight: Time has passed since we released Jive Copilot, and perceptions may have changed.
  - This needs verification with customers.
  - Some of the pushback on Jive Copilot was around use of OpenAI specifically, since it is external to AWS. In the meantime Bedrock has improved significantly, and may provide a more palatable alternative. Copilot was built to support multiple LLM providers.
  - We can use LLMs to provide value in the form of automatic content archiving.
  - We can also improve Jive Copilot significantly by switching to an agentic approach (which was nascent at the time we built Copilot).
- Insight: Despite the completion of Jive Unity, we will still need to run a subset of the legacy microservices that are used by legacy HOP customers who have not upgraded.
  - While the services can be scaled back due to the reduced usage, this continued usage will prevent realizing the full cost optimization outcomes of Jive Unity.
- Insight: There are many opportunities for reducing technical debt in Jive:
  - Preventing certificate expiry due to the lack of auto-renew plus the lack of documentation. Remove unnecessary certificates.
  - Addressing gaps in the release and deployment process for non-core components.
  - Removing unnecessary microservices and other non-core components, which will result in cost reduction.
  - Improving technical documentation.
- Insight: Due to the content archiving problem and the poor quality of the existing search functionality, combined with broad customer rejection of generative AI at a base level, we need to provide a more modern search feature with semantic matching capability.
- Insight: All types of customers can be made to upgrade:
  - For SaaS customers, by modifying their contract so that it explicitly states that upgrades are mandatory within a given time period of release.
  - For customers with on-prem deployments, by completely phasing out support for the legacy microservices, meaning portions of their Jive will stop working.
- Insight: Jive has core capabilities that, if broken, will certainly cause customer churn:
  - Storing and organizing content for the long term.
  - Providing a broadcast communication system (outside of email or slack).
  - Backwards compatibility of the Jive API.
- Insight: Jive is comprised of a core, single-tenant web application and activity engine, surrounded by multiple multi-tenant microservices, which should be kept isolated from each other:
  - Use separate clusters, don't co-host multiple microservices together.
  - There are several advantages: better separation of concerns, operational simplicity, and minimization of blast radius in event of any cluster-level problems (i.e. operational issues with semantic search will be confined there and not affect other components).
- Insight: The Jive mobile app was originally created at a time when mobile web browsers were less fully featured, and web technologies supporting responsive design were nascent. However today, there is little reason for a native mobile app for a product like Jive. The web application is already partially responsive and this can be improved.

# Experts

- **Adam Grant** [@AdamMGrant](https://x.com/AdamMGrant): An organizational psychologist, professor at Wharton, and best-selling author, Adam Grant is one of the most influential voices on workplace psychology and employee engagement. He is known for his research-based insights on motivation, purpose, feedback, and leadership. Grant is also a keynote speaker at major conferences, including Workhuman Live 2025
- **Jacob Morgan **[@jacobm](https://x.com/jacobm): A futurist and employee experience strategist, Jacob Morgan is recognized for his thought leadership on the future of work and employee engagement. He shares research-driven trends and practical strategies, often based on interviews with global executives
- **Meghan M. Biro** [@MeghanMBiro](https://x.com/MeghanMBiro): As the founder of TalentCulture and a prominent HR tech analyst, Meghan M. Biro is known for her expertise in workplace culture, technology, and engagement. Her commentary is widely followed in the HR community
- **Daniel Pink** [@DanielPink](https://x.com/DanielPink): Author of Drive, which explores the concepts of autonomy, mastery and purpose as driving forces behind employee motivation. Posts about motivation, leadership, and workplace dynamics.
- **Simon Sinek** [@simonsinek](https://x.com/simonsinek): Author and speaker Simon Sinek is renowned for his work on leadership and purpose, particularly his concept of "Start With Why," which has influenced how organizations think about engagement and meaning at work
- **Josh Bersin **[@Josh_Bersin](https://x.com/Josh_Bersin): One of the world’s leading HR analysts, Josh Bersin provides in-depth research and commentary on employee engagement, learning, and organizational culture
- **Bev Kaye **[@BeverlyLKaye](https://x.com/BeverlyLKaye): A pioneer in talent retention and engagement, Bev Kaye has decades of experience helping organizations grow and retain their people through practical tools and strategies
- **Ian Hutchinson** [@IanHutchinson\_](https://x.com/IanHutchinson_): An Australian-based expert, Ian Hutchinson is an award-winning speaker, author, and consultant with over 20 years of experience in employee engagement. He is known for his innovative programs and his focus on creating self-responsible workplace cultures
- **David Green **[@david_green_uk](https://x.com/david_green_uk): A leading expert in people analytics, David Green explores how data and analytics can drive better employee engagement and business decisions. He is a frequent keynote speaker and writer on HR technology, workforce analytics, and AI-driven HR strategies
- **Liz Ryan **[@humanworkplace](https://x.com/humanworkplace): Founder of Human Workplace, Liz Ryan is an HR leader who advocates for more human-centric and empathetic workplaces. She regularly shares actionable insights and challenges outdated HR practices.
- **Mallory Herrin** [@Herrin_HR](https://x.com/Herrin_HR): CEO and Principal HR Consultant at HerrinHR, Mallory Herrin is recognized for her expertise in HR technology selection and implementation, including employee engagement software. She is a thought leader in aligning HR tech with organizational strategy
- **Christina Moran** [@dr_cmoran](https://x.com/dr_cmoran): An industrial/organizational psychologist, Dr. Moran brings expertise in people leadership, business operations, and the strategic use of HR technology to drive engagement
- **Jenny Podewils** (Leapsome Co-CEO) [@jennypodewils](https://x.com/jennypodewils): Focuses on scaling businesses and developing people through technology-enabled engagement and performance management platforms
- **Anthony Onesto** (Chief People Officer at Suzy) [@anthonyonesto](https://x.com/anthonyonesto): Specializes in talent management and the impact of generational shifts on employee engagement technology
- **Amy C. Edmondson** [@AmyCEdmondson](https://x.com/AmyCEdmondson): Harvard professor known for psychological safety and its impact on engagement.

# DOK1/DOK2 - Knowledge Tree

## **Jive HOP, Jive Cloud and Jive Unity**

- Summary: Jive Unity is a strategy of merging two legacy Jive products, with a common ancestor, back into a single product.
- Fact: Historically there were two separate Jive products: Jive HOP (hosted and on-prem) and Jive Cloud (see [Background here](https://docs.google.com/document/d/1pPVbp5VNy-cUfAGic4DAtXxYjqNGDJSCsPZpez6RdGI/edit?tab=t.0#heading=h.k1jug1hefskt)). These were forked from the same original codebase, and modified in different ways (primarily Jive Cloud). However, their high-level feature sets are very similar, and their technical implementations also retain similarity in many areas.
- Fact: Jive Unity is a strategy, currently in the final stages of the main Engineering phase, which is combining Jive HOP and Jive Cloud into a single product with the superset of functionality from both products (see [Jive Unity feature strategy specification](https://docs.google.com/document/d/1pPVbp5VNy-cUfAGic4DAtXxYjqNGDJSCsPZpez6RdGI/edit?tab=t.0)).
- Fact: Jive Unity is based on the Jive HOP codebase, incorporating elements from Jive Cloud in order to port the functionality (see the [unity/base branch in the Jive HOP GitHub repository](https://github.com/trilogy-group/jive-hop-custom/tree/unity/base)).
- Fact: Jive Unity is being deployed to a new production environment in a new production AWS account (see [production spec](https://docs.google.com/document/d/1jMG5TnDYS2ZQqnHjgkLDvzCpjAtmYfWdXTeA-bIknDo/edit?tab=t.0)), supported by new dev/QA environments in a new non-production AWS account (see [non-production spec](https://docs.google.com/document/d/1fMyawEuicPos3f2JKfKX25C6RhJzyCv0z6Tl2WUMUos/edit?tab=t.0)).

## **Customers**

- Summary: Jive customers are highly varied, in terms of size, business domain, and usage of Jive. Many Jive customers are very slow to upgrade or change, which helps for customer retention, but means customers are using outdated versions of the software.
- Fact: There are three distinct groups of Jive customers (see [overview here](https://docs.google.com/document/d/1pPVbp5VNy-cUfAGic4DAtXxYjqNGDJSCsPZpez6RdGI/edit?tab=t.0#heading=h.8chcrbpzm3tq)):
  - On-Prem customers, who use Jive HOP in their own environments, operated and monitored internally by the customer. We have very little visibility of these Jive instances; some are within moated networks with no Internet access.
  - Hosted customers, who use Jive HOP but are hosted by us.
  - Cloud customers, who use Jive Cloud, which is hosted by us.
- Fact: Jive Unity will eventually, by replacing two products with one, reduce the number of groups of Jive customers from three to two:
  - On-Prem customers, for whom the result of Jive Unity is simply a major version upgrade to their existing Jive instance(s). Depending on their level of customization, this may be a trivial upgrade or a significant effort.
  - SaaS customers, which includes all former Hosted and Cloud customers.
- Fact: Jive Unity includes migrating all Cloud customers to the new environment, but migrating Hosted customers, while this is also a major upgrade, requires more specific efforts due to the nature of customization of their existing instances (source: discussions with customers).
- Fact: Jive customers range from small trusts to large enterprises and government organizations (source: [ARR by customer](https://docs.google.com/spreadsheets/d/1mMrVbjTvl0seo8Kv8nHkoTt5Jw7yE7uJFWcUcRLWKZc/edit?gid=1963088695#gid=1963088695)).
- Fact: Jive customers come from many different business domains, for example automotive manufacturers, banks, insurance companies, military organizations, government departments, retailers, charities, etc (source: [ARR by customer](https://docs.google.com/spreadsheets/d/1mMrVbjTvl0seo8Kv8nHkoTt5Jw7yE7uJFWcUcRLWKZc/edit?gid=1963088695#gid=1963088695)).
- Fact: The majority of ARR comes from larger enterprise and government customers (source: [ARR by customer](https://docs.google.com/spreadsheets/d/1mMrVbjTvl0seo8Kv8nHkoTt5Jw7yE7uJFWcUcRLWKZc/edit?gid=1963088695#gid=1963088695)).
- Fact: Different Jive customers have different levels of customization, from vanilla instances with default layouts and a simple logo change, to instances that are customized in ways that make it difficult to upgrade (source: direct examination of Jive instances, accessed via [JCA](https://aws.prod.jivehosted.com/)).
- Fact: Many Jive customers were reluctant to adopt Jive Copilot, citing FUD about, and policies against, generative AI. This was in 2024 (source: [release tracker](https://docs.google.com/spreadsheets/d/1Snb9m3vLS7f__CanpufGgLnjbjvr30q8P7nihbjblOU/edit#gid=2116362989) showing the complete rollback of the feature).
- Fact: While there are exceptions, most Jive customers are resistant to upgrading. For customers hosting their own instances, we do not have visibility of which versions they are using, except where there are customer support tickets (source: [JCA](https://aws.prod.jivehosted.com/)).
- Fact: Customization of Jive causes friction for upgrading.
- Fact: Many customers have rigorous change control processes, which result in simple bureaucracy adding latency, in some cases up to a year (source: discussions with customers).
- Fact: Only some customers use analytics. Only some customers use gamification ([source](https://docs.google.com/document/d/1RlRcXTd2-IUt9trQugkNw3rI-mE5Hh68wjbW9jxkbxA/edit?tab=t.0#heading=h.q1gcn7pnrzgx)). Only some customers use video. Many see these features as ancillary. All customers rely on Jive to store and organize content for the long term.
- Fact: Breaking legacy customizations will cause customers to churn, because they will consider other options since they need to move anyway.
- Fact: Customers rely on the [Jive API](https://developers.jivesoftware.com/api/v3/cloud/rest/index.html).

## **Users**

- Summary: Jive follows a standard pattern of having users who are highly engaged and contribute frequently, down to users who never use the platform. Language support is focused on European and Asian languages.
- Fact: Jive users can be classified according to their usage (see [admin console](https://thrive.ignitetech.com/admin/user-search.jspa)):
  - Administrators are those who control Jive access, structure, moderation, and configuration.
    - Administrators may or may not also use Jive themselves as end users.
  - Power Users are those who drive the usage of Jive within their organization. These users can be identified using analytics and gamification statistics (if enabled).
    - Power Users are very important to the viability of Jive, since they drive engagement and continued usage of the platform.
  - Frequent Publishers are not power users but do make contributions to the content in their Jive instance.
  - Consumers are users who predominantly search for and view content, but rarely engage beyond likes and occasional comments.
  - Disengaged Users are those who rarely login to Jive, or who might only visit the home page (this is possible if Jive is the company-enforced home page on employee web browsers).
- Fact: Unified Jive supports a range of European and Asian languages, all of which are LTR languages ([source](https://github.com/trilogy-group/jive-hop-custom/blob/master/core/src/main/resources/), [docs](https://docs.jivesoftware.com/getting_started/JiveinTranslation#supported-languages)).
- Fact: Legacy Jive Cloud supported two RTL languages ([docs](https://docs.jivesoftware.com/getting_started/JiveinTranslation#supported-languages)), but this feature was not used by any customer instances ([analysis](https://github.com/trilogy-group/jive-hop-custom/issues/7636)).
- Fact: Jive users are predominantly English speaking, but in some communities, a number of other languages are used. For SaaS customers, these are mainly European languages (French, Spanish, German) ([source](https://docs.google.com/spreadsheets/d/1wFZErSOLRVta9ghiDyrTRONs_q0LQKFuan380GFpXdo/edit?gid=0#gid=0)).

## **Use Cases**

- Summary: Jive is an employee engagement platform. It helps new workers onboard and assimilate, it is a system of record for many types of information, and it provides features to entice users to contribute to the platform.
- Fact: Jive produces value for customers by reducing the time and effort required to onboard new hires and transfers ([website](https://www.jivesoftware.com/product/deployment#gsc.tab=0)).
- Fact: Jive produces value for customers by providing a single, long-term repository for all types of internal information and communications ([website](https://www.jivesoftware.com/product/features#gsc.tab=0)).
- Fact: Jive has a variety of features ([source](https://github.com/trilogy-group/jive-hop-custom/)):
  - Jive can be a document repository, for customers to store and reference policies, procedures and other long-term documentation.
  - Jive can be a company wiki, allowing exchange and development of ideas in a semi-structured manner.
  - Jive can be used to send announcements from leadership to all staff.
  - Jive can be a staff discussion forum.
  - Jive has project management and documentation capabilities.
  - Jive has engagement and gamification features.
  - Jive has analytics capabilities, so that leaders can see the interactions between people and departments, the engagement of workers across the organization, and the growth of the internal community.
  - [Jive has a REST API](https://developers.jivesoftware.com/api/v3/cloud/rest/index.html) that supports almost all actions that non-admin users can perform through the web UI.
  - Jive has an AI assistant, [Jive Copilot](https://docs.google.com/document/d/1sR-Cspest13EZVUDQc2YlvBZZsyOoBsJhop06lpe-vs/edit), which can be used to help users discover and summarize content in the Jive instance.
- Fact: Customers use Jive in a variety of ways in different combinations. Some customers use only a portion of Jive's functionality, while others use a wide range of its capabilities (source: investigation of Jive instances, and discussions with customers).

## **Technical Architecture**

- Summary: Jive is a monolithic, single tenant web application, coupled with an activity engine, and surrounded by optional multi tenant microservices that provide activity-specific functionality. Jive is highly configurable and customizable, which leads to it being difficult for some customers to upgrade.
- Fact: Jive consists of several high-level components (see [documentation on Brewspace](https://brewspace.jiveland.com/docs/DOC-287894)):
  - A monolithic core web application. This is what users primarily interact with. This is a single-tenant (installation per Jive instance) application.
  - An activity engine. Unified Jive uses EAE (Enterprise Activity Engine), which is a single-tenant solution inherited from legacy Jive HOP. Legacy Jive Cloud had its own activity engine named "R2E2"; this was made redundant by Jive Unity.
  - An application-level cache. This is one of many caches used throughout the architecture, but in this case it is a single-tenant, first-class citizen alongside the web application and the activity engine.
  - Various multi-tenant microservices, providing ancillary functionality. There are a large number of such microservices; some examples include:
    - Search.
    - Analytics.
    - Gamification (Jive Rewards).
    - Video transcoding.
    - Video transcription.
    - Jive Copilot, an built-in AI assistant.
- Fact: Jive components communicate predominantly through HTTP APIs.
- Fact: Nearly all Jive components are Java-based ([source](https://github.com/trilogy-group/jive-hop-custom/tree/unity/base)).
  - The Jive web application runs on Java 8 and is based on Spring Framework 5.3. These are both near EOL.
  - Other components run on various different versions of Java, primarily Java 8.
- Fact: Upgrading to Spring Framework 6 requires upgrading to Java 17+ ([reference](https://github.com/spring-projects/spring-framework/wiki/Spring-Framework-Versions#jdk-version-range)).
- Fact: The Jive UI uses jQuery ([source](https://github.com/search?q=repo%3Atrilogy-group%2Fjive-hop-custom%20jquery&type=code)) and lodash ([source](https://github.com/search?q=repo%3Atrilogy-group%2Fjive-hop-custom+_.&type=code)) extensively.
- Fact: Unified Jive is hosted on ECS and Fargate, with databases in Central DB ([specification](https://docs.google.com/document/d/1pFa0IToDtV8Rf8Qt-PYUjM18vFU7ccW61V8Ccgn9PFs/edit?tab=t.0#heading=h.7vlxwdpvsb4g)).
- Fact: Jive microservices are hosted in a range of different AWS infrastructure, from EC2 instances to serverless deployments.
- Fact: Jive databases can be PostgreSQL, MySQL, Microsoft SQL Server or Oracle Database ([support matrix](https://thrive.ignitetech.com/docs/DOC-385420)). SaaS instances use PostgreSQL.
- Fact: User-uploaded attachments, images and videos are stored via storage provider in either file storage or cloud storage (with several backends including the default of S3), depending on configuration ([source](https://github.com/trilogy-group/jive-hop-custom/blob/a4c6af1c283df440280a7d592fd21dc89335a06a/core/src/main/java/com/jivesoftware/eos/StorageProvider.java#L35)).
  - There is also a database-backed storage provider, but storing large binary files in the database is not recommended.
- Fact: Jive does not transform the core content in a meaningful way, it acts as an information repository, with content creation, presentation of content and interactive features such as liking and commenting.
- Fact: Jive's important processing is of activity events. That is, whenever users interact with content (by viewing, liking, sharing, editing, commenting, etc), an event is emitted that is then fed into analytics, gamification and other components ([documentation on Brewspace](https://brewspace.jiveland.com/docs/DOC-100459)). These are relatively simple aggregation algorithms.

## **Data Structures**

- Summary: The Jive data entities are focused on Content of various types, and Places into which that content is organized.
- Fact: At the core of the Jive data schema is the **Content** entity. The primary related database table is `JiveContent` ([source](https://github.com/trilogy-group/jive-hop-custom/blob/a4c6af1c283df440280a7d592fd21dc89335a06a/core/src/main/java/com/jivesoftware/community/JiveContentObject.java#L19)). There are many different types of content entity:
  - Questions
  - Discussions
  - Blog Posts
  - Files
  - Documents
  - Polls
  - Status Updates
  - Tasks
  - Messages
  - Videos
  - Events
  - Ideas
- Fact: Content items of most types share many common features (source: examination of the Jive user interface):
  - A unique URL per content item.
  - A plain text title.
    - For Messages, this is the subject line.
  - A rich text body / description, edited by users with TinyMCE wysiwyg editor.
    - For Tasks and Messages, the description is entered as plain text.
    - For Status Updates, the number of formatting options is greatly reduced.
  - Ability to add tags and categories.
  - Ability to set access control.
  - Like and Share buttons.
  - Threaded comments, which each can also be Liked and Shared.
- Fact: Content items of most types have specific features (source: examination of the Jive user interface):
  - Comments on Questions are considered Answers, and can be marked as Helpful or Correct.
  - Comments on Discussions can also be marked as Helpful.
  - Blog Posts can be associated with either a Place or a user's personal blog, and includes some additional options such as banners and text styling.
  - Files are uploaded files encapsulated as a first-class entity.
  - Documents could be considered the "base" content type.
  - Polls allow the creator to define a set of options, visitors to vote for one of those options, and then results to be collated and shared.
  - Status Updates are simple, short messages in a microblogging style.
  - Tasks can belong to Projects, and each Task has an assignee and a due date.
  - Messages are plain text messages sent directly from one user to another user or list of users.
  - Videos are either embedded or uploaded video files, displayed with a built-in video.js player, and captioning if enabled.
  - Events have a date and time, capacity, guest list, and ability for users to register for the event.
  - Ideas invite users to vote for them, which can then potentially influence project or organizational decisions and strategies. These could be small ideas or large ideas.
- Fact: The second important element in the data schema is the **Place** entity ([source](https://github.com/trilogy-group/jive-hop-custom/blob/a4c6af1c283df440280a7d592fd21dc89335a06a/plugins/extendedApis/src/main/java/com/jivesoftware/extendedApis/entities/v1/Place.java#L11)).
  - There are three types of Place:
    - Spaces are the primary structure of a Jive community.
      - Spaces are places for related content.
      - Spaces can be mapped to organizational structures such as divisions, departments and teams, or to products and services, or to geographical regions, etc.
      - The community itself is the root space, and the other spaces form a hierarchical structure from that root.
    - Social Groups are for common interests that are not necessarily aligned to organizational structures. This could be the company knitting group or chess club, or for employees working on AI side projects.
      - Social Groups are not aligned to the structure of Spaces.
    - Projects are goal-focused places.
      - Projects are typically aligned to real-world organization projects.
      - Projects exist within the Space structure, that is, every Project is a child of either the community itself, or a specific Space.
      - Projects typically contain Tasks.
- Fact: The different types of Places are represented by multiple different tables in the database, and as a result, there is no actual referential integrity between Content and Places (source: examination of the database).
  - These references are made using `containertype` and `containerid` columns. Depending on the value of `containertype` , the `containerid` refers to a record in one table or another.
  - [This code](https://vscode.dev/github/trilogy-group/jive-hop-custom/blob/master/core/src/javascript/core-api/src/core/Place.js#L71-L82) demonstrates selecting the right `containertype` value based on the type of place.
  - Code relating to container types is strewn throughout the code, with over 11,000 search results for "containertype" in the Jive HOP web application code.
  - Spaces are stored in the `JiveCommunity` database table.
  - Social Groups are stored in the `JiveSGroup` database table.
  - Projects are stored in the `JiveProject` database table.
- Fact: Non-relational data is also used for User Preferences (`JiveUserProp` table), which identifies the property itself with a plain text `name` column ([source](https://github.com/trilogy-group/jive-hop-custom/blob/a4c6af1c283df440280a7d592fd21dc89335a06a/core/src/main/java/com/jivesoftware/community/user/preferences/action/UserPreferencesAction.java)).

## Content Discovery and the Archiving Problem

- Summary: Jive builds up content over the years, which when coupled with a poor quality search engine, results in it being very difficult for users to discover content. Archiving the old content takes up-front and ongoing manual effort.
- Fact: Content discovery is an important capability of Jive, because of the volume of content that is possible in large instances. This is true even for active content, but it is made much worse by the presence of many over a decade of historical content building up (source: discussions with customers).
- Fact: Archiving content inherently takes effort on the customer's part.
- Fact: Jive does not provide any native automation to assist with archiving old content. Such an automation could potentially be built (by a customer) outside of Jive, performing its task using the Jive API ([source](https://github.com/trilogy-group/jive-hop-custom/tree/unity/base)).
- Fact: Jive provides a search subsystem, which uses an adapter approach to support multiple different search backends ([source](https://github.com/trilogy-group/jive-hop-custom/tree/unity/base/core/src/main/java/com/jivesoftware/community/search)):
  - In legacy Jive Cloud, only a cloud-hosted ElasticSearch-based solution was available.
  - In legacy Jive HOP, and inherited into unified Jive, both on-prem Solr and cloud-based ElasticSearch solutions are available. (Note this is a similar but different implementation to the Jive Cloud search backend)
- Fact: None of the available Jive search adapters work very well (source: customer feedback and personal experience).
  - They are all keyword-based, with boolean operators to control how those keywords are used (e.g. "software AND (development OR engineering)").
  - Customers complain about content discovery being a major problem.
  - This was one of the reasons Jive Copilot was created, in order to help users find content without relying on their accurate use of the existing search engine.

## **Integrations**

- Summary: Jive is capable of integrating with authentication and office systems natively, as well as any other systems via plugins.
- Fact: Jive integrates with authentication and SSO systems, via SAML and OAuth2 ([documentation](https://docs.jivesoftware.com/administering_your_community/configuring_authentication_methods/SSOSAMLConfiguringIdPs)).
- Fact: Jive integrates with legacy Office, legacy Outlook, their Office365 replacements, and Sharepoint ([documentation](https://docs.jivesoftware.com/jive_integrations/office_and_productivity_tools/OfficeOnlineHowTos)).
- Fact: Jive supports custom integrations with any other system via plugins.

## **Customization**

- Summary: Jive is highly configurable and customizable, with multiple different "layers" of related capabilities. The look and feel, layout and content of the Jive instance can be heavily customized, within certain predefined templates.
- Fact: Jive has multiple extension and customization points, as a result of its long history and layers of development ([source](https://github.com/trilogy-group/jive-hop-custom/tree/unity/base)):
  - The first approach implemented was the ability to provide a "Custom WAR" file, which overrides the base application.
    - This approach is still used by some large customers.
    - This causes major friction when upgrading, since any changes to the application itself may result in changes to the patches in the custom WAR file.
    - In legacy Jive, this was only available to Jive HOP customers (both Hosted and On-Prem), it was never supported on Jive Cloud.
    - In unified Jive, this capability is hidden from legacy Jive Cloud customers.
  - The Plugins approach was developed to replace custom WAR files, however:
    - Plugins can be enabled, disabled and configured through the Jive admin console, but it still requires adding the plugin source code to the Jive instance.
    - Plugins can break with major Jive version upgrades.
    - In legacy Jive, plugins were only available to Jive HOP customers.
    - Internally, legacy Jive Cloud has a concept of plugins that was inherited from the common ancestor, however there was no way for administrators to install or remove plugins, the functionality appeared to be core.
    - In unified Jive, plugins can only be installed if the capability is enabled, which it will not be for customers who are migrating from Jive Cloud.
    - Plugins can be used to extend the core functionality of Jive in any way required, from simple integrations with external systems, to completely changing aspects of Jive's core operation.
  - Add-ons (extensions) is the latest approach, and has some core differences:
    - Add-ons can be added directly through the user interface, there is no need to deploy Java code directly to the server(s) running Jive.
    - Add-ons can be added from a Jive-managed "Registry" or by uploading the code directly.
    - Unlike custom WAR files and plugins, add-ons / extensions do not change Jive's core behavior; they are only overlaid.
    - In legacy Jive, add-ons were available for both Jive HOP and Jive Cloud.
    - In unified Jive, add-ons remain the preferred extension mechanism.
- Fact: The layout of Space, Project and Social Group pages can be customized, with page administrators being able to determine the placement of various types of information within the page (source: Jive user interface). However, there are two different native constructs used to provide this functionality, based on configuration:
  - Widgets is a legacy approach, and is limited to a single "Overview" page per Place ([specification](https://docs.google.com/document/d/1BRbPDPd47r0QpcoobAvoeLUgPGz1tI1x_KP7zRyYct0/edit?tab=t.0)).
  - Tiles is the recommended approach. There are some tiles built in, and others are provided by add-ons, aka extensions ([specification](https://docs.google.com/document/d/11PBKSHd3-c2lxX39Z3zaaAND4VNgyDxYB74UYRzK1qA/edit?pli=1&tab=t.0)). When enabled, Tiles can be used on the "Overview" page as well as additional pages that can be created per-place.
  - The layout of both Widget pages and Tile pages are restricted to a set of predefined options.
- Fact: The look and feel can be customized using a theming engine and/or advanced theming techniques (source: Jive user interface).
- Fact: While we have full visibility of SaaS instances (via [JCA](https://aws.prod.jivehosted.com/)), we have zero visibility of customization in Jive on-prem (customer-hosted) instances.
- Fact: Jive Copilot can (like many Jive features) be independently enabled or disabled ([source](https://github.com/trilogy-group/jive-hop-custom/blob/a4c6af1c283df440280a7d592fd21dc89335a06a/war/src/main/webapp/WEB-INF/classes/template/global/admin/settings-copilot.ftl#L107-L123)).
- Fact: Of 69 legacy Jive Cloud instances analyzed, only 18 have enabled Copilot, and 13 instances have left it on "Standby", which periodically nags users and administrators about enabling it. The remaining 38 have proactively disabled the feature. ([source](https://docs.google.com/spreadsheets/d/1wFZErSOLRVta9ghiDyrTRONs_q0LQKFuan380GFpXdo/edit?gid=707416189#gid=707416189&range=A28:D34))

## **Operations and Maintenance**

- Summary: Jive has operational issues, due to poor documentation, a long history of upgrades being skipped, and customers refusing to upgrade.
- Fact: Many components of Jive are not well understood operationally (see [blank pages in Confluence](https://trilogy-confluence.atlassian.net/wiki/spaces/JIVE/pages/499546369/Jive+HOP+Architecture)).
  - For example, for many of the microservices, there is no known working mechanism for deploying changes.
  - The communication between the microservices is not well mapped out or documented.
- Fact: Despite recent upgrade efforts ([specification](https://docs.google.com/document/d/1penvEscrc_hbjOCQr_kKt4Uk_-b0c_rnFLUbP6Gbg_E/edit)), there are still many upgrades to complete:
  - Spring Framework was upgraded, the next step is to upgrade the Java runtime itself (the most fundamental upgrade possible for Jive) and then we can upgrade Spring Framework again to the latest version.
  - We have upgraded many UI libraries but others, including lodash, are yet to be upgraded.
  - We need to continue to support more recent OS and database platforms ([support matrix](https://thrive.ignitetech.com/docs/DOC-385420)).
  - The upgrades to date have focused on the core web application and EAE only; the microservices are similarly out of date.
- Fact: Jive uses many SSL certificates, even applying encryption to internal communications between Jive components.
  - Many of the SSL certificates used by Jive do not auto-renew.
  - Fact: The SSL certificates used by Jive are not well understood or documented.
- Fact: While On-Prem Jive is hosted and operated by the customer, depending on configuration, it may use some of the cloud-based microservices, for example:
  - Legacy Jive HOP has a "Cloud Search" option, which uses AWS-hosted ElasticSearch.
  - Legacy Jive HOP has a "Cloudalytics" option, which extends the built-in analytics capabilities to match those in Jive Cloud, by utilizing some of the same infrastructure with a different interface for Jive HOP applications.
  - As part of Jive Unity, we are adding Jive Rewards integration, which will use the same microservice as previously integrated with legacy Jive Cloud.

## **Mobile Applications and Browser Extensions**

- Summary: Jive has a mobile application, available for both Android and iOS, but it has not been recently upgraded or improved.
- Fact: Jive has a mobile application, known various as "Jive Daily", "Jive Mobile" and "Jive for [Android/iOS]" ([source](https://github.com/trilogy-group/jive-hop-android_daily_jive_9)).
- Fact: Jive has a browser extension, "Jive Anywhere", which allows users to share content they find online directly to their Jive community without needing to open the full Jive web application ([reference](https://docs.google.com/document/d/1rvF437VA7oetLq8KajMFSCuvhIvxjoI7XyZH6Y-RZg8/edit?tab=t.0)).
- Fact: Both the Jive mobile application (Play store) ([specification](https://docs.google.com/document/d/1VS00Z2NhdhHtRngfdMqp7Rq08WrRESUbxrWWFB0frQs/edit)) and browser extension (Chrome store) ([specification](https://docs.google.com/document/d/1rvF437VA7oetLq8KajMFSCuvhIvxjoI7XyZH6Y-RZg8/edit)) have been removed from their stores due to lack of access to and notifications from the controlling account.
- Fact: The Jive mobile application (both iOS and Android versions) is based on an old technical stack and has not had significant work for multiple years ([source](https://github.com/trilogy-group/ps-jive-mobile-responsive/commits/master/)).
- Fact: The Jive mobile application does not have feature parity with the web version ([reference](https://docs.google.com/document/d/1MXUfa510RMqgp4CsFwGkdghUxSPfb7v3ueORKotfh4Y/edit?tab=t.0)),
- Fact: The Jive web application uses some elements of responsive design, meaning that the layout changes based on the screen dimensions. However, this is not applied consistently ([reference](https://docs.google.com/document/d/1i5JjXxrdcFBxZP7wa-WzFYUzFesQrDI_6MHOgmOAfV4/edit?tab=t.0)).

## **Compliance and Risk**

- Summary: Jive has a relatively standard security compliance requirement, a standard GDPR requirement, and enforced accessibility (WCAG) requirements.
- Fact: Jive instances often contain confidential and proprietary information, that customers rightly do not want exfiltrated (source: discussions with customers).
- Fact: Access control within Jive can be very fine-grained, allowing user groups or individual users to be allowed or denied access to Places at any level. This allows users to share information with the whole company, and to store information in Jive that is only visible to themselves or a small group (source: Jive user interface).
- Fact: Jive instances are primarily used by employees of and contractors to the customer organization. External users can be added on an individual basis; there is no "publicly accessible" option (source: Jive user interface).
- Fact: Jive does not have specific compliance requirements for code, release process or deployments. However, customers do scan their instances (both SaaS and self-hosted) and report relevant vulnerabilities (CVEs, etc).
- Fact: Jive is hosted in the EU for some customers and therefore must remain GDPR compliant.
- Fact: Jive is required to remain accessible, including compliance with WCAG 2.2 AA or above ([specification](https://docs.google.com/document/d/1OrMXWQUh9TPmazIMMyatWJTvHbNp03tw7emwDOZsPBI/edit?tab=t.0)). This relates to the application itself; users might still create content with poor accessibility.
- Fact: There is currently no mechanism to continuously verify accessibility requirements.
