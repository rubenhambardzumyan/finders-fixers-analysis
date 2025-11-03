# Test Transcript Scenarios - Key

## Overview
This folder contains 5 test transcript scenarios designed to evaluate AI detection of different BrainLift creation patterns and expert identification.

## Case Breakdown

### Case 1: Direct Assignment
- **Pattern**: "I need you to build a BrainLift"
- **Situation**: Client onboarding process standardization
- **Participants**:
  - **Ruben Hambardzumyan** (Manager) - Identifies the problem and assigns the task
  - **Eugene Dolgov** (Expert) - Has the best track record with client satisfaction, assigned to build the BrainLift
- **Key Test**: Clear direct assignment to a specific person with reasoning

### Case 2: Vague "You" Reference
- **Pattern**: "You should build a BrainLift"
- **Situation**: API documentation standardization
- **Participants**:
  - **Marcus Chen** (Leader) - Identifies the need and makes vague assignment
  - **Sarah Williams** (Team Member) - Notices documentation issues
  - **David Rodriguez** (Backend Team) - Experiences support burden from poor docs
- **Key Test**: AI must determine who "you" refers to (likely Marcus addressing the whole group or Sarah specifically)

### Case 3: Multiple Person Options
- **Pattern**: "A or B or C needs to build a BrainLift"
- **Situation**: Customer retention strategy
- **Participants**:
  - **Jennifer Park** (Leader) - Identifies need for customer retention BrainLift
  - **Alex Thompson** (Expert 1) - Has survey data and customer feedback analysis
  - **Maria Gonzalez** (Expert 2) - Has customer journey mapping expertise
  - **Lisa Chang** (Expert 3) - Has retention metrics and success patterns
- **Key Test**: AI must identify that multiple qualified candidates exist, each with complementary expertise

### Case 4: Collective Responsibility
- **Pattern**: "We should build a BrainLift"
- **Situation**: DevOps deployment process improvement
- **Participants**:
  - **Tom Baker** (Team Member) - Has security compliance requirements
  - **Rachel Kim** (Team Member) - Knows monitoring setup
  - **Mike Johnson** (Team Member) - Knows rollback procedures
- **Key Test**: AI must recognize collaborative knowledge building scenario where team pools expertise

### Case 5: Implicit Need Detection
- **Pattern**: No explicit BrainLift mention
- **Situation**: Machine Learning model performance review
- **Participants**:
  - **Dr. Amanda Foster** (Leader) - Identifies performance concerns
  - **Kevin Liu** (Expert 1) - Deep learning expertise, neural networks
  - **Sophie Martinez** (Expert 2) - PhD in hybrid recommendation systems
  - **James Wilson** (Team Member) - Infrastructure/operations perspective
  - **Rebecca Chen** (Expert 3) - Experience at Google, Netflix, Spotify with similar systems
- **Key Test**: AI must detect implicit BrainLift opportunity with 3 clear experts (Kevin, Sophie, Rebecca) despite no explicit mention

## Testing Objectives
1. **Pattern Recognition**: Can AI identify different linguistic patterns for BrainLift suggestions?
2. **Context Analysis**: Can AI determine assignments from context when references are vague?
3. **Expertise Identification**: Can AI identify who has relevant knowledge for building BrainLifts?
4. **Implicit Detection**: Can AI recognize BrainLift opportunities without explicit mentions?
5. **Multi-person Scenarios**: Can AI handle complex scenarios with multiple potential builders?