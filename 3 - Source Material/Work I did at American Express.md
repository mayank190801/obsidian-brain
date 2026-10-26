In depth knowledge about it is important for sure... (basic)

- Achieved reduction in ETL flow load times by 96%, from 5 minutes to under 10 seconds, by optimizing API performance and refining the UI layout, significantly enhancing the user experience for over 1,000 platform users.

You can explain the below one nicely ~ We have a confluence page for this 

- Innovated a BigQuery Optimizer that provided actionable insights for optimizing ETL flows. The tool improved 60% of production processes by suggesting optimizations such as partition and cluster pruning, removing redundant encryptions, and eliminating unused columns, which led to a patent filing for its innovative design.

Knowledge 

Using Abstract Syntax Tree and Visitor Pattern provided by ZetaSQL, we have written logic for checking all these conditions for our Query Optimiser 

**ZetaSQL** is a framework for parsing, analyzing, and executing SQL queries, developed by Google. It serves as the foundation for Google’s internal and external data processing systems like **BigQuery**, **Spanner**, and **Cloud SQL**.

ZetaSQL can parse SQL queries and produce an abstract syntax tree (AST) that represents the structure of the query.

 ZetaSQL can analyze SQL queries for semantic correctness and provide detailed error messages for common issues.

**Use Visitor Pattern**: ZetaSQL provides a visitor pattern to traverse the AST. You can create a custom visitor by extending zetasql::ASTVisitor. This allows you to define behavior for each type of node.

**Traverse the AST**: After creating your custom visitor, you can traverse the AST by calling Accept() on the root node.

In ZetaSQL, when using the Visitor pattern:
• You define a visitor class that overrides methods for specific node types.
• Each overridden method is where you specify what to do when that node type is encountered.

```
class MyVisitor extends ASTVisitor {
    @Override
    public void visit(ASTNode node) {
        // Pre-processing logic (optional)

        // Traverse child nodes
        for (ASTNode child : node.getChildren()) {
            child.accept(this);  // Recursively accept the visitor
        }

        // Post-processing logic (optional)
    }

    @Override
    public void visitSelectStatement(ASTSelectStatement node) {
        // Handle specific logic for select statements
        super.visitSelectStatement(node); // This can optionally call the base implementation
    }
}
```

• The Visitor pattern typically involves a **depth-first traversal** of the AST.
• Each node can have a pre-processing step before visiting its children and a post-processing step after visiting its children.
• This allows you to implement custom logic for each type of node while managing the traversal effectively.

-> Add here what you exactly did with those ASTTrees (simple as that)


- Spearheaded the end-to-end development of a feature for exporting ETL flows directly to Google Cloud Storage (GCS) from BigQuery, designing the frontend UI in React and implementing the backend using Spring Boot. This increased data export efficiency by 30% and managed over 2TB of data daily.

- Increased test coverage for the query optimizer module from 0% to 91.2% using Mockito and JUnit.

- Analyzed and resolved ZetaSQL compatibility issues on ARM laptops for 20+ team members using Docker Buildx.