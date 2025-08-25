![Pharo](https://pharo.org/web/files/pharo-2x.png)

# Google Summer of Code'25 Final Report: Pharo
* **Contributor:** [Alok Pathak](https://github.com/Alokzh)
* **Organisation:** [Pharo](https://pharo.org)
* **Sub-Organisation:** [pharo-containers](https://github.com/pharo-containers)
* **Project:** [Implementation of Standard Data Structures & Algorithms](https://summerofcode.withgoogle.com/programs/2025/projects/JNhTr4F3)
* **Mentors:** [Sebastian Jordan Montaño](https://github.com/jordanmontt), [Gordana Rakic](https://github.com/gocko), [Stéphane Ducasse](https://github.com/Ducasse)

## 1. Project Overview

Pharo lacked robust, well-designed implementations of fundamental data structures, with existing collections being weakly supported and inconsistently designed. This project developed a comprehensive library of essential data structures, including Buffers, Stacks, and various Trees (Binary Search Tree, AVL Tree, Red-Black Tree etc.).

The result is a flexible, extensible, and production-ready framework with consistent APIs, thorough documentation, and comprehensive test coverage that enhances developer productivity across the Pharo ecosystem.

## 2. Summary of Accomplishments

Over Three months, significant progress was made implementing and enhancing core data structures across multiple repositories, focusing on performance, robust design, and seamless Pharo integration.

### Key Contributions by Repository

### Containers-Buffer
**Repository:** [Containers-Buffer](https://github.com/pharo-containers/Containers-Buffer)

**What:** A high-performance, fixed-capacity circular buffer with both FIFO (First-In, First-Out) and LIFO (Last-In, First-Out) variants.

**How:** The implementation uses a pre-allocated collection and pointers that wrap around the ends, providing O(1) complexity for all operations. It is optimized for streaming data and designed to minimize garbage collection events.

**Why:** Offers a massive performance advantage over OrderedCollection for use cases like managing chat histories, undo/redo functionality, where elements are continuously added and removed.

**Technical Deep Dive:** Created a comprehensive analysis comparing DataFrames vs Buffers for large dataset processing, demonstrating when each approach excels. [Read the full comparison](https://github.com/pharo-containers/Containers-Buffer/blob/main/docs/DataFrame%20vs%20Buffer.md)

### Containers-BinarySearchTree
**Repository:** [Containers-BinarySearchTree](https://github.com/pharo-containers/Containers-BinarySearchTree)

**What:** A complete Binary Search Tree (BST) was implemented from the ground up, providing a foundational ordered data structure.

**How:** It features an efficient node architecture and supports multiple traversal methods (in-order, pre-order, post-order), range queries, and full compliance with Pharo's collection protocol. A Null Object Pattern (NilNode) was used to eliminate null checks, resulting in cleaner and more robust algorithms.

**Why:** This provides a baseline for ordered data management and serves as the foundation for more complex, self-balancing trees. It's ideal for scenarios where input data is expected to be random.

### Container-AVL
**Repository:** [Container-AVL](https://github.com/pharo-containers/Container-AVL)

**What:** A self-balancing binary search tree that guarantees logarithmic performance.

**How:** The implementation automatically rebalances the tree after insertions and deletions using rotations, ensuring the height difference between sibling subtrees is never more than one. It also integrates with a visual inspector for easier debugging and visualization.

**Why:** Crucial for applications requiring guaranteed O(log n) worst-case performance for lookups and updates, such as in database indexing or real-time systems where performance predictability is key.

### Containers-RedBlackTree
**Repository:** [Containers-RedBlackTree](https://github.com/pharo-containers/Container-RedBlackTree)

**What:** A production-ready self-balancing tree that offers an excellent trade-off between strict balancing and performance.

**How:** Balances the tree by enforcing a set of "Red-Black" properties (e.g., a red node cannot have a red child). This typically requires fewer rotations on insertion/deletion compared to AVL trees.

**Why:** It is one of the most common balanced trees used in production systems (like C++ STL's std::map), offering guaranteed O(log n) performance with slightly faster insertion and deletion times than AVL trees on average.

### Containers-Stack
**Repository:** [Containers-Stack](https://github.com/pharo-containers/Containers-Stack)

**What:** The existing Stack implementation was enhanced with dynamic growth capabilities and a more robust API.

**How:** The stack can now automatically expand its capacity when needed, preventing overflow errors. It maintains O(1) complexity for push, pop, and top operations while ensuring efficient memory management.

**Why:** This makes the Stack more reliable and versatile for general-purpose programming, such as in parsers, compilers, and expression evaluation, where the required stack depth is unknown beforehand.

### Other Contributions
**Repository:** [Containers-OrderedSet](https://github.com/pharo-containers/Containers-OrderedSet)

**Contribution:** Minor improvements and test enhancements.

### Complete List of Contributions
All pull requests submitted during the Google Summer of Code period can be viewed here:
* [View All 25 Pull Requests on GitHub](https://github.com/pulls?page=1&q=is%3Apr+author%3AAlokzh+org%3Apharo-containers)

### Comparison of Tree Data Structures
The Table below summarizes the key differences between the implemented Tree structures:

| Feature | Binary Search Tree (BST) | AVL Tree | Red-Black Tree |
|---------|---------------------------|----------|----------------|
| **Search Time** | O(log n) avg, O(n) worst | O(log n) guaranteed | O(log n) guaranteed |
| **Insert Time** | O(log n) avg, O(n) worst | O(log n) guaranteed | O(log n) guaranteed |
| **Delete Time** | O(log n) avg, O(n) worst | O(log n) guaranteed | O(log n) guaranteed |
| **Balance Guarantee** | None (depends on input order) | Strictly balanced (height diff ≤ 1) | Less strictly balanced |
| **Rebalancing** | None | Frequent rotations (up to 2 per op) | Fewer rotations (up to 3 per op) |
| **Best Use Case** | Simple ordered data where input is random and worst-case performance is not a concern | Read-heavy applications where fast lookups are critical and insertions/deletions are less frequent | Write-heavy or mixed-use applications where both lookups and modifications are frequent |

## 3. Current State of the Project

All implemented data structures are in a production-ready state:

**Complete:** Containers-Buffer, Containers-Stack, Containers-BinarySearchTree, Container-AVL, and Containers-RedBlackTree are functionally complete.

**Tested:** All implementations have comprehensive test suites covering core functionality, edge cases, and property validation.

**Documented:** Each repository's README has been updated with examples and API explanations.

**Integrated:** All structures follow Pharo's collection protocols, ensuring seamless integration into the broader ecosystem.

## 4. What's Left to Do (Future Work)
This project has built a strong foundation, but there are clear next steps for continued development:

### Implement New Data Structures
- **Improve & Extend:** Enhance the existing repositories for BTree, Trie, KeyedTree, etc., by adding more features, optimizing performance, improving documentation & test coverage.
- **B+ Tree Implementation:** A variation of the B-Tree that maintains all values at the leaf level, improving range query performance
- **Deque (Double-ended Queue):** Valuable for algorithms requiring efficient additions and removals from both ends

### Enhance Tooling and Visualization  
- **Visual Inspectors:** Extend the AVL Tree's visual inspector to Binary Search Tree and Red-Black Tree for educational & debugging purposes

- **Benchmarking Suite:** Develop a standardized benchmarking framework to formally compare the performance of these new data structures against each other and against Pharo's core collections under various workloads.

### Ecosystem-wide Improvements
- **CI and Documentation:** Contribute to improving the Continuous Integration (CI) setup and README documentation across all [pharo-containers](https://github.com/pharo-containers) repositories to ensure long-term maintainability and ease of use for new contributors.

## 5. Challenges and Key Takeaways
This project was a tremendous learning experience that presented several interesting challenges and offered valuable lessons.

### Challenges Faced

**Mastering Complex Algorithms:** Implementing the rebalancing logic for AVL and Red-Black trees was challenging. It required a deep, theoretical understanding to ensure every rotation & color-flip was correct.

**Designing a Polymorphic API:** Creating a consistent and intuitive API across different types of trees, required careful thought about abstraction and design patterns.

### Key Takeaways

**The Power of TDD:** Test-Driven Development helps ensure code quality and correctness. Writing tests first made it possible to tackle complex logic with confidence and provided a safety net for refactoring.

**Clean Code and Design Patterns:** The use of the Null Object Pattern in trees was a revelation. It simplified the code dramatically by removing conditional checks, leading to more readable and less error-prone algorithms.

**Community Collaboration:** The feedback from my mentors on pull requests was invaluable. It taught me how to write clearer code, communicate technical ideas effectively, and collaborate within an established open-source community.

## 6. Pharo Resources & Links
For those interested in learning more about Pharo or getting involved with the community, here are some essential links:
- [**Official Website**](https://pharo.org)
- [**Community Discord**](https://discord.com/invite/QewZMZa)
- [**GitHub Repos**](https://github.com/pharo-project)

## 7. Acknowledgments
These past few months have been so wonderful. I am extremely grateful to my Mentors, **Sebastian Jordan Montaño**, **Gordana Rakic** & **Stéphane Ducasse**. They helped me with every implementation doubts, code reviews, and guided me throughout the project. I hope the work done here will be useful to the entire Pharo community.

Lastly, Thnx to Google & Pharo Org for providing me this great opportunity !