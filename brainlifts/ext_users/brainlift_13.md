Jive Unity - Playbox
Owner
Felipe Schloegl ﻿felipe.schloegl﻿
https://ephor.ai/join/e650d811
Purpose
Playbox is a feature that allows for a gamification implementation that aims to increase community activity in order to increase content creation and interactions with the platform.
Goal: Unite Cloud-only Playbox gamification with Jive Unity, giving missions, badges, challenges and leader-boards while re-using Unity’s existing event stream.
Benefits:
Cloud unique features will be supported now on Unity, allowing for a more seamless migration into the unified Jive version.
Maintenance Efficiency: Consolidates maintenance and improvement efforts into a single platform, reducing operational costs. This unification allows for a single point of focus on maintenance and improvement compared to the 2 fronts (HOP and Cloud) previously present.
Improved User Experience: Provides a unified and engaging experience, increasing user satisfaction
Out of Scope:
Replacing Status Level, it will be disabled when playbox is enabled but it is still available after the migration and all related data to Status Level should be kept when upgrading or migrating into Jive Unity
Cloud Playbox Feature Migration: All Cloud Playbox features will be migrated to Unity, except for advanced analytics, which will be handled separately.
Expected Outcomes:
Provide feature parity between Cloud and Unity
Provide seamless migration to users
Provide complete data migration to be performed by DevOps
DOK4 - SPOV
Gamification must feel fair, fast and visible.
SPOV: Gamification systems should prioritize real-time feedback over delayed rewards.
Connection to Insight: Event-Stream Convergence
Zero-tolerance for data loss or corruption during migrations.
Missing scores, badges or missing erodes trust faster than nothing at all; migrations must achieve maximum data fidelity and run tests to make sure no data is left behind.
Connection to Insight: Production Database Safety
Multi-tenant Data Isolation:
Migration scripts must use instance-specific filters (e.g., tenantId) when inserting directly into production Playbox databases to prevent cross-contamination between instances.
Connection to Insight: Production Database Safety
DOK3 - Insights
Jive Unity and Jive Cloud unification:
Event-Stream Convergence
Insight: Using similar structure for event handling can help using the same structure for multiple purpose like playbox and Status Level gamifications. This will help with reducing maintenance complexity. No functionalities changes will be expected, focus only on maintenance reduction.
Strategic Analysis: This convergence not only streamlines maintenance but also enables real-time feedback, supporting SPOV: Gamification must feel fair, fast and visible
Quantifiable Outcomes: Expected reduction in maintenance costs
Source: High-level overview: https://github.com/trilogy-group/jive-hop-custom/docs/jive-unity/playbox/unity-playbox-documentation.md
Connection to SPOV: Supports Gamification must feel fair, fast and visible.
