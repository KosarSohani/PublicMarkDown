---


---

<h1 id="oracle-database-concepts">Oracle Database Concepts</h1>
<h2 id="introduction-to-oracle-database">1 Introduction to Oracle Database</h2>
<p>Oracle Database is a robust RDBMS with features for scalability (sharding), multitenancy (CDB/PDB), and high availability. It supports SQL, PL/SQL, and Java for data access and application logic.</p>
<h3 id="relational-databases">1 Relational Databases</h3>
<ul>
<li>
<p>Every organization has information that it must store and manage to meet its requirements. This information must be available to those who need it.</p>
</li>
<li>
<p>A  <strong>Database Management System (DBMS)</strong>  controls data storage, organization, and retrieval.<br>
Elements: Kernel code, metadata repository (data dictionary), query language.</p>
</li>
<li>
<p><strong>Relational Model</strong>: Defined by E.F. Codd (1970), based on mathematical set theory.</p>
<ul>
<li><strong>Major Aspects</strong>: Structures, operations, and integrity rules govern data.</li>
</ul>
</li>
<li>
<p><strong>RDBMS</strong>: Manages data in tables (relations) with logical (application) and physical (internal) operations.</p>
</li>
<li>
<p><strong>Brief History of Oracle Database</strong>:</p>
<ul>
<li><strong>1979</strong>: First commercial SQL-based RDBMS (Oracle V2).</li>
<li><strong>Key milestones</strong>: PL/SQL (Oracle7), object-relational support (Oracle8i), cloud (Oracle 12c), stability (Oracle 19c).</li>
</ul>
</li>
<li>
<p><strong>Schema Objects</strong></p>
<ul>
<li>
<p>Logical structures (e.g., tables, indexes) independent of physical storage.</p>
</li>
<li>
<p><strong>Tables</strong>: Store data in rows (instances) and columns (attributes).</p>
</li>
<li>
<p><strong>Indexes</strong>: Improve query performance; logically independent of data.</p>
</li>
</ul>
</li>
<li>
<p><strong>Data Access</strong></p>
<ul>
<li>
<p><strong>SQL</strong>: Declarative language for querying/modifying data.</p>
</li>
<li>
<p><strong>PL/SQL &amp; Java</strong>: Procedural extensions for server-side logic.</p>
</li>
</ul>
</li>
<li>
<p><strong>Transaction Management</strong></p>
<ul>
<li>
<p><strong>Transactions</strong>: Atomic units of work (all-or-nothing).</p>
</li>
<li>
<p><strong>Data Concurrency</strong>: Locks prevent conflicts in multiuser environments.</p>
</li>
<li>
<p><strong>Data Consistency</strong>: Ensures users see committed data (no “dirty reads”).</p>
</li>
</ul>
</li>
<li>
<p><strong>Oracle Database Architecture</strong></p>
<ul>
<li>
<p><strong>Database and Instance</strong>:</p>
<ul>
<li>
<p><strong>Database</strong>: Physical files (data, control, redo logs).</p>
</li>
<li>
<p><strong>Instance</strong>: Memory structures (SGA, PGA) and background processes.</p>
</li>
</ul>
</li>
<li>
<p><strong>Multitenant Architecture</strong>:</p>
<ul>
<li>
<p><strong>CDB (Container Database)</strong>: Hosts multiple  <strong>PDBs (Pluggable Databases)</strong>.</p>
</li>
<li>
<p><strong>Benefits</strong>: Cost reduction, easier management, isolation.</p>
</li>
</ul>
</li>
<li>
<p><strong>Sharding Architecture</strong>:</p>
<ul>
<li>Horizontal partitioning across databases (“shards”) for scalability.</li>
</ul>
</li>
<li>
<p><strong>Storage Structures</strong>:</p>
<ul>
<li>
<p><strong>Physical</strong>: Data files, control files, redo logs.</p>
</li>
<li>
<p><strong>Logical</strong>: Blocks → extents → segments → tablespaces.</p>
</li>
</ul>
</li>
<li>
<p><strong>Processes &amp; Memory</strong>:</p>
<ul>
<li>
<p>Client, server, and background processes.</p>
</li>
<li>
<p><strong>SGA</strong>  (shared memory) and  <strong>PGA</strong>  (process-specific memory).</p>
</li>
</ul>
</li>
<li>
<p><strong>Application Architecture</strong>:</p>
<ul>
<li><strong>Client-server</strong>  vs.  <strong>multitier</strong>  (e.g., SOA, SODA for schemeless apps).</li>
</ul>
</li>
<li>
<p><strong>Networking</strong>: Oracle Net Services handles communication (TCP/IP, HTTP).</p>
</li>
</ul>
</li>
</ul>
<h1 id="part-i-oracle-relational-data-structure">Part I: Oracle Relational Data Structure</h1>
<p>This part describes the basic data structures of a database, including data integrity rules, and the structures that store metadata.</p>
<h2 id="tables-and-table-clusters">2 Tables and Table Clusters</h2>
<p>This chapter provides an introduction to schema objects and discusses tables, which are the most common types of schema objects.</p>
<h3 id="introduction-to-schema-objects">1 Introduction to Schema Objects</h3>
<ul>
<li><strong>Schema</strong>: Logical container for data structures (tables, indexes, etc.)
<ul>
<li>Owned by a database user</li>
<li>Example: HR schema with employees table</li>
</ul>
</li>
<li><strong>Schema Object Types</strong>:
<ul>
<li><strong>Tables</strong>: Store data in rows (most common).</li>
<li><strong>Indexes</strong>: Speed up data retrieval.</li>
<li><strong>Views</strong>: Virtual tables based on queries.</li>
<li><strong>Partitions</strong>: Divide large tables/indexes into manageable pieces.</li>
<li><strong>Sequences</strong>: Generate unique numbers (e.g., for primary keys).</li>
<li><strong>Synonyms</strong>: Aliases for schema objects.</li>
<li><strong>PL/SQL subprograms</strong>: Named PL/SQL blocks (procedures, packages).</li>
</ul>
</li>
<li><strong>Storage</strong>:
<ul>
<li>Some objects store data in segments (tables, indexes)</li>
<li>Others are metadata-only (views, sequences)</li>
</ul>
</li>
<li><strong>Dependencies</strong>: Objects can reference other objects (views depend on tables)</li>
<li><strong>System Schemas</strong>:
<ul>
<li><strong>SYS</strong>: Base data dictionary</li>
<li><strong>SYSTEM</strong>: Additional administrative data</li>
</ul>
</li>
</ul>
<h3 id="overview-of-tables">2 Overview of Tables</h3>
<h4 id="table-types">Table Types</h4>
<ul>
<li><strong>Relational Tables</strong>: Standard row/column structure</li>
<li><strong>Attribute-Clustered Tables</strong>: An attribute-clustered table is a heap-organized table that stores data in close proximity on disk based on user-specified clustering directives. The directives specify columns in single or multiple tables.</li>
<li><strong>Temporary Tables</strong>: A temporary table holds data that exists only for the duration of a transaction or session.</li>
<li><strong>External Tables</strong>: An external table accesses data in external sources as if this data were in a table in the database.</li>
<li><strong>Blockchain Tables</strong>: A blockchain table is an append-only table designed for centralized blockchain applications.</li>
<li><strong>Immutable Tables</strong>: Immutable tables are read-only tables that prevent unauthorized data modifications by insiders and accidental data modifications resulting from human errors.</li>
<li><strong>Object Tables</strong>: An object table is a special kind of table in which each row represents an object.</li>
</ul>
<h4 id="table-organization">Table Organization</h4>
<ul>
<li><strong>Heap-Organized</strong> (default): Unordered storage</li>
<li><strong>Index-Organized</strong>: Ordered by primary key</li>
</ul>
<h4 id="table-components">Table Components</h4>
<ul>
<li><strong>Columns</strong>: Define attributes
<ul>
<li>Data types (VARCHAR2, NUMBER, DATE, etc.)</li>
<li><strong>Virtual columns</strong>: Computed on demand (no storage).</li>
<li><strong>Invisible columns</strong>: Hidden unless explicitly queried.</li>
</ul>
</li>
<li><strong>Rows</strong>: Individual records</li>
<li><strong>Constraints</strong>:
<ul>
<li>Primary keys</li>
<li>Foreign keys</li>
<li>Check constraints</li>
<li>NOT NULL</li>
</ul>
</li>
</ul>
<h4 id="table-storage">Table Storage</h4>
<ul>
<li>Segments in tablespaces; rows stored in data blocks.</li>
<li>Compressed formats available:
<ul>
<li><strong>Basic compression</strong>: This type of compression is intended for bulk load operations. The database does not compress data modified using conventional DML. You must use direct path INSERT operations, ALTER TABLE . . . MOVE operations, or online table redefinition to achieve basic table compression.</li>
<li><strong>Advanced compression</strong>: This type of compression is intended for OLTP applications and compresses data manipulated by any SQL operation. The database achieves a competitive compression ratio while enabling the application to perform DML in approximately the same amount of time as DML on an uncompressed table.</li>
<li><strong>Hybrid Columnar compression</strong>: With Hybrid Columnar Compression, the database stores the same column for a group of rows together. The data block does not store data in row-major format, but uses a combination of both row and columnar methods.</li>
</ul>
</li>
</ul>
<h3 id="table-clusters">3 Table Clusters</h3>
<p>A table cluster is a group of tables that share common columns and store related data in the same blocks.</p>
<h4 id="types-of-clusters">Types of Clusters</h4>
<ul>
<li><strong>Indexed Clusters</strong>:
<ul>
<li>An index cluster is a table cluster that uses an index to locate data. The cluster index is a B-tree index on the cluster key. A cluster index must be created before any rows can be inserted into clustered tables.</li>
<li>Example: Employees and departments clustered by department_id</li>
</ul>
</li>
<li><strong>Hash Clusters</strong>:
<ul>
<li>A hash cluster is like an indexed cluster, except the index key is replaced with a hash function. No separate cluster index exists. In a hash cluster, the data is the index.</li>
<li>Example: Quick lookup by department_id</li>
</ul>
</li>
</ul>
<h4 id="benefits">Benefits</h4>
<ul>
<li>Reduced I/O for joins</li>
<li>Improved access time for related data</li>
<li>More efficient storage</li>
</ul>
<h4 id="limitations">Limitations</h4>
<p>Not ideal for frequently updated tables or full scan.</p>
<h3 id="specialized-table-types">4 Specialized Table Types</h3>
<h4 id="attribute-clustered-tables">Attribute-Clustered Tables</h4>
<p>An attribute-clustered table is a heap-organized table that stores data in close proximity on disk based on user-specified clustering directives. The directives specify columns in single or multiple tables.</p>
<ul>
<li><strong>Linear Order</strong>: A linear ordering scheme for a table divides rows into ranges based on user-specified attributes in a specific order. Oracle Database supports linear ordering on single or multiple tables that are connected through a primary-foreign key relationship. Optimized for prefix column queries.</li>
<li><strong>Interleaved Order</strong>: Optimized for varied column combinations</li>
</ul>
<h5 id="benefits-1">Benefits</h5>
<p>I/O reduction, better compression, no index overhead.</p>
<h4 id="temporary-tables">Temporary Tables</h4>
<p>A temporary table holds data that exists only for the duration of a transaction or session. Data in a temporary table is private to the session. Each session can only see and modify its own data.</p>
<ul>
<li><strong>Global Temporary Tables</strong>:
<ul>
<li>Definition visible to all sessions</li>
<li>Data private to session/transaction</li>
</ul>
</li>
<li><strong>Private Temporary Tables</strong>:
<ul>
<li>Definition and data private to session</li>
<li>Prefixed with ORASPTT_</li>
</ul>
</li>
</ul>
<h5 id="purpose">Purpose</h5>
<p>Temporary tables are useful in applications where a result set must be buffered.</p>
<h4 id="external-tables">External Tables</h4>
<p>An external table accesses data in external sources as if this data were in a table in the database. The data can be in any format for which an access driver is provided. You can use SQL (serial or parallel), PL/SQL, and Java to query external tables.<br>
External tables are useful when an Oracle database application must access non-relational data.</p>
<ul>
<li><strong>Supported formats</strong>
<ul>
<li>Text files</li>
<li>JSON</li>
<li>Hadoop (HDFS)</li>
<li>Object stores</li>
</ul>
</li>
<li><strong>Access drivers</strong>: ORACLE_LOADER, ORACLE_DATAPUMP, etc.</li>
</ul>
<h4 id="blockchain-tables">Blockchain Tables</h4>
<p>A blockchain table is an append-only table designed for centralized blockchain applications.</p>
<ul>
<li><strong>Features</strong>
<ul>
<li>Cryptographic row chaining</li>
<li>Retention periods</li>
<li>Verification procedures</li>
</ul>
</li>
</ul>
<h4 id="immutable-tables">Immutable Tables</h4>
<p>Immutable tables are read-only tables that prevent unauthorized data modifications by insiders and accidental data modifications resulting from human errors.</p>
<h4 id="object-tables">Object Tables</h4>
<p>An object table is a special kind of table in which each row represents an object and stores instances of object types.</p>
<ul>
<li>Example:<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">CREATE</span> <span class="token keyword">TYPE</span> department_typ <span class="token keyword">AS</span> OBJECT <span class="token punctuation">(</span>d_name VARCHAR2<span class="token punctuation">(</span><span class="token number">100</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">CREATE</span> <span class="token keyword">TABLE</span> departments_obj_t <span class="token keyword">OF</span> department_typ<span class="token punctuation">;</span>

</code></pre>
</li>
</ul>
<h2 id="indexes-and-index-organized-tables">3 Indexes and Index-Organized Tables</h2>
<p>Indexes are schema objects that can speed access to table rows. Index-organized tables are tables stored in an index structure.</p>
<h3 id="introduction-to-indexes">1 Introduction to Indexes</h3>
<ul>
<li>An <strong>index</strong> is an optional structure associated with a table or table cluster that can speed data access.</li>
<li>Indexes are logically and physically independent of the data in the objects they are associated with.</li>
<li>Dropping an index does not affect applications but may slow access to previously indexed data.</li>
</ul>
<h4 id="advantages-and-disadvantages-of-indexes">Advantages and Disadvantages of Indexes</h4>
<p><strong>Advantages:</strong></p>
<ul>
<li>Fast access path to a single row of data.</li>
<li>Reduces disk I/O by avoiding full table scans.</li>
</ul>
<p><strong>Disadvantages:</strong></p>
<ul>
<li>Requires deep knowledge of data model and application.</li>
<li>Requires maintenance as data changes.</li>
<li>Occupies disk space.</li>
<li>Performance overhead during DML operations.</li>
</ul>
<h4 id="index-usability-and-visibility">Index Usability and Visibility</h4>
<ul>
<li><strong>Usability</strong>: An unusable index is ignored by the optimizer and not maintained by DML operations.</li>
<li><strong>Visibility</strong>: An invisible index is maintained by DML but not used by the optimizer by default.</li>
</ul>
<h4 id="keys-and-columns">Keys and Columns</h4>
<ul>
<li>A <strong>key</strong> is a set of columns or expressions used to build an index.</li>
<li>Indexes and keys are different: indexes are physical structures, while keys are logical concepts.</li>
</ul>
<h4 id="composite-indexes">Composite Indexes</h4>
<ul>
<li>An index on multiple columns in a table.</li>
<li>Column order is important for query performance.</li>
</ul>
<h4 id="unique-and-nonunique-indexes">Unique and Nonunique Indexes</h4>
<ul>
<li><strong>Unique indexes</strong>: Guarantee no duplicate values in key columns.</li>
<li><strong>Nonunique indexes</strong>: Permit duplicate values.</li>
</ul>
<h4 id="types-of-indexes">Types of Indexes</h4>
<p>Oracle provides several indexing schemes:</p>
<ul>
<li>B-tree indexes (standard).</li>
<li>Bitmap indexes.</li>
<li>Function-based indexes.</li>
<li>Application domain indexes.</li>
</ul>
<h4 id="how-the-database-maintains-indexes">How the Database Maintains Indexes</h4>
<ul>
<li>Indexes are automatically maintained and updated during DML operations.</li>
<li>Many indexes on a table can degrade DML performance.</li>
</ul>
<h4 id="index-storage">Index Storage</h4>
<ul>
<li>Index data is stored in an index segment.</li>
<li>Indexes can be stored in a separate tablespace for easier administration.</li>
</ul>
<h3 id="overview-of-b-tree-indexes">2 Overview of B-Tree Indexes</h3>
<ul>
<li>B-trees (balanced trees) are the most common type of database index.</li>
<li>Provide excellent retrieval performance for exact match and range searches.</li>
</ul>
<h4 id="branch-blocks-and-leaf-blocks">Branch Blocks and Leaf Blocks</h4>
<ul>
<li><strong>Branch blocks</strong>: Used for searching.</li>
<li><strong>Leaf blocks</strong>: Store key values and rowids.</li>
</ul>
<h4 id="index-scans">Index Scans</h4>
<ul>
<li><strong>Full Index Scan</strong>: Reads the entire index in order.</li>
<li><strong>Fast Full Index Scan</strong>: Accesses data in the index without accessing the table.</li>
<li><strong>Index Range Scan</strong>: Ordered scan with conditions on leading columns.</li>
<li><strong>Index Unique Scan</strong>: Retrieves a single row.</li>
<li><strong>Index Skip Scan</strong>: Uses logical subindexes of a composite index.</li>
<li><strong>Index Clustering Factor</strong>: Measures row order relative to an indexed value.</li>
</ul>
<h4 id="reverse-key-indexes">Reverse Key Indexes</h4>
<ul>
<li>Physically reverses bytes of each index key to distribute inserts evenly.</li>
</ul>
<h4 id="ascending-and-descending-indexes">Ascending and Descending Indexes</h4>
<ul>
<li><strong>Ascending</strong>: Stores data in ascending order (default).</li>
<li><strong>Descending</strong>: Stores data in descending order.</li>
</ul>
<h4 id="index-compression">Index Compression</h4>
<ul>
<li><strong>Prefix Compression</strong>: Compresses portions of primary key column values.</li>
<li><strong>Advanced Index Compression</strong>: Improves on prefix compression with adaptive algorithms.</li>
</ul>
<h3 id="overview-of-bitmap-indexes">3 Overview of Bitmap Indexes</h3>
<ul>
<li>Stores a bitmap for each index key.</li>
<li>Suitable for low-cardinality columns and read-only environments.</li>
</ul>
<h4 id="bitmap-indexes-on-a-single-table">Bitmap Indexes on a Single Table</h4>
<ul>
<li>Efficient for queries on columns with few distinct values (e.g., gender).</li>
</ul>
<h4 id="bitmap-join-indexes">Bitmap Join Indexes</h4>
<ul>
<li>A bitmap index for the join of two or more tables.</li>
<li>Reduces data volume by performing restrictions in advance.</li>
</ul>
<h4 id="bitmap-storage-structure">Bitmap Storage Structure</h4>
<ul>
<li>Uses a B-tree structure to store bitmaps for each indexed key.</li>
</ul>
<h3 id="overview-of-function-based-indexes">4 Overview of Function-Based Indexes</h3>
<ul>
<li>Computes the value of a function or expression and stores it in an index.</li>
<li>Can be B-tree or bitmap indexes.</li>
</ul>
<h4 id="uses-of-function-based-indexes">Uses of Function-Based Indexes</h4>
<ul>
<li>Efficient for evaluating statements with functions in WHERE clauses.</li>
<li>Example: Index on <code>UPPER(first_name)</code> for case-insensitive searches.</li>
</ul>
<h4 id="optimization-with-function-based-indexes">Optimization with Function-Based Indexes</h4>
<ul>
<li>Optimizer may use an index range scan for queries with expressions.</li>
</ul>
<h3 id="overview-of-application-domain-indexes">5 Overview of Application Domain Indexes</h3>
<ul>
<li>Customized index specific to an application.</li>
<li>Useful for complex data types like documents, spatial data, and images.</li>
</ul>
<h3 id="overview-of-index-organized-tables">6 Overview of Index-Organized Tables</h3>
<ul>
<li>Tables stored in a B-tree index structure.</li>
<li>Rows are stored in an index defined on the primary key.</li>
</ul>
<h4 id="index-organized-table-characteristics">Index-Organized Table Characteristics</h4>
<ul>
<li>Differences from heap-organized tables:
<ul>
<li>No separate primary key index.</li>
<li>Logical rowids for secondary indexes.</li>
<li>Cannot be stored in a table cluster.</li>
</ul>
</li>
</ul>
<h4 id="index-organized-tables-with-row-overflow-area">Index-Organized Tables with Row Overflow Area</h4>
<ul>
<li>Allows splitting a row into an index entry and an overflow part.</li>
</ul>
<h4 id="secondary-indexes-on-index-organized-tables">Secondary Indexes on Index-Organized Tables</h4>
<ul>
<li>Uses logical rowids based on primary key.</li>
<li><strong>Logical Rowids and Physical Guesses</strong>: Physical guesses can speed access.</li>
<li><strong>Bitmap Indexes on Index-Organized Tables</strong>: Uses a heap-organized mapping table.</li>
</ul>
<h2 id="partitions-views-and-other-schema-objects">4 Partitions, Views, and Other Schema Objects</h2>
<p>This chapter discusses various schema objects in Oracle Database, including partitions, views, materialized views, sequences, dimensions, and synonyms.</p>
<h3 id="overview-of-partitions">1 Overview of Partitions</h3>
<p><strong>Partitioning</strong> decomposes large tables and indexes into smaller, manageable pieces called <strong>partitions</strong>.</p>
<ul>
<li>Each partition is an independent object with its own name and storage characteristics.</li>
</ul>
<h4 id="benefits-of-partitioning">Benefits of Partitioning</h4>
<ul>
<li><strong>Increased availability</strong>: Unavailability of a partition does not affect the entire object.</li>
<li><strong>Easier administration</strong>: DDL statements can manipulate partitions individually.</li>
<li><strong>Reduced contention</strong>: Distributes DML operations over many segments.</li>
<li><strong>Enhanced query performance</strong>: Speeds up ad hoc queries in data warehouses.</li>
</ul>
<h4 id="partition-characteristics">Partition Characteristics</h4>
<p>Each partition must have the same logical attributes (column names, data types, constraints).</p>
<ul>
<li><strong>Partition Key</strong>: Determines which partition each row belongs to.</li>
</ul>
<h4 id="partitioning-strategies">Partitioning Strategies</h4>
<ul>
<li><strong>Range Partitioning</strong>: Maps rows based on ranges of values (e.g., dates).</li>
<li><strong>Interval Partitioning</strong>: Automatically creates partitions for data exceeding existing ranges.</li>
<li><strong>List Partitioning</strong>: Uses discrete values to assign rows to partitions.</li>
<li><strong>Hash Partitioning</strong>: Uses a hashing algorithm to distribute rows evenly.</li>
<li><strong>Reference Partitioning</strong>: Child table partitions based on a foreign key relationship with a parent table.</li>
<li><strong>Composite Partitioning</strong>: Combines two partitioning methods (e.g., range-list, range-hash).</li>
</ul>
<h4 id="partitioned-tables">Partitioned Tables</h4>
<p>A partitioned table consists of one or more partitions managed individually.</p>
<ul>
<li><strong>Segments for Partitioned Tables</strong>: Each partition is stored in its own segment.</li>
<li><strong>Compression for Partitioned Tables</strong>: Partitions can be stored in compressed format.</li>
</ul>
<h4 id="partitioned-indexes">Partitioned Indexes:</h4>
<ul>
<li><strong>Local Partitioned Indexes</strong>: Index is partitioned the same way as its table.</li>
<li><strong>Global Partitioned Indexes</strong>: Index is partitioned independently of the table.</li>
<li><strong>Partial Indexes</strong>: Indexes only specific partitions of a table.</li>
</ul>
<h3 id="overview-of-sharded-tables">2 Overview of Sharded Tables</h3>
<p><strong>Sharding</strong> breaks large tables into smaller pieces (<strong>shards</strong>) stored in multiple databases.<br>
Each shard is hosted on a dedicated server with its own resources.</p>
<ul>
<li><strong>Sharded Tables</strong>: Tables partitioned across shards based on a sharding key (e.g., <code>customer_id</code>).</li>
<li><strong>Tablespace Sets</strong>: Logical units of data distribution in a sharded database.</li>
</ul>
<h3 id="overview-of-views">3 Overview of Views</h3>
<p>A <strong>view</strong> is a stored query that logically represents one or more tables.</p>
<ul>
<li>Views are used to:
<ul>
<li>Provide additional security by restricting access to specific rows or columns.</li>
<li>Hide data complexity (e.g., joins or calculations).</li>
<li>Present data differently from the base tables.</li>
<li>Isolate applications from changes in base table definitions.</li>
</ul>
</li>
</ul>
<h4 id="characteristics-of-views">Characteristics of Views</h4>
<p>Views do not store data; they derive data from base tables.</p>
<ul>
<li><strong>Data Manipulation in Views</strong>: Users can query and, with restrictions, perform DML on views.</li>
<li><strong>How Data Is Accessed</strong>: The database merges view queries with user queries for optimization.</li>
</ul>
<h4 id="updatable-join-views">Updatable Join Views</h4>
<p>Join views with multiple tables can permit DML operations if they meet specific criteria.</p>
<h4 id="object-views">Object Views</h4>
<p>Virtual object tables where each row is an instance of an object type.</p>
<ul>
<li>Useful for prototyping or transitioning to object-oriented applications.</li>
</ul>
<h3 id="overview-of-materialized-views">4 Overview of Materialized Views</h3>
<p>A <strong>materialized view</strong> stores the result of a query as a schema object.</p>
<ul>
<li>Used in data warehouses, replication, and mobile computing environments.</li>
</ul>
<h4 id="characteristics-of-materialized-views">Characteristics of Materialized Views</h4>
<ul>
<li>Store actual data and consume storage space.</li>
<li>Can improve performance through query rewrite.</li>
</ul>
<h4 id="refresh-methods">Refresh Methods:</h4>
<ul>
<li><strong>Complete Refresh</strong>: Re-executes the defining query.</li>
<li><strong>Incremental Refresh</strong>: Processes only changes to existing data.</li>
<li><strong>In-Place and Out-of-Place Refresh</strong>: Refreshes directly on the view or using outside tables.</li>
</ul>
<h4 id="query-rewrite">Query Rewrite</h4>
<p>Transforms user queries to use materialized views for faster performance.</p>
<h3 id="overview-of-sequences">5 Overview of Sequences</h3>
<p>A <strong>sequence</strong> generates unique integers for surrogate keys.</p>
<ul>
<li><strong>Sequence Characteristics</strong>: Defines intervals, caching, and cycling behavior.</li>
<li><strong>Concurrent Access</strong>: Multiple users can generate unique numbers without contention.</li>
</ul>
<h3 id="overview-of-dimensions">6 Overview of Dimensions</h3>
<p><strong>Dimensions</strong> categorize data for business analysis (e.g., time, geography).</p>
<ul>
<li><strong>Hierarchical Structure</strong>: Defines parent/child relationships (e.g., city → state → country).</li>
<li><strong>Creation of Dimensions</strong>: Defined using <code>CREATE DIMENSION</code> with levels, hierarchies, and attributes.</li>
</ul>
<h3 id="overview-of-synonyms">7 Overview of Synonyms</h3>
<p>A <strong>synonym</strong> is an alias for a schema object (e.g., table, view, sequence).</p>
<ul>
<li><strong>Public Synonyms</strong>: Accessible by all users.</li>
<li><strong>Private Synonyms</strong>: Restricted to a specific user’s schema.</li>
<li>Simplify SQL statements and hide object locations.</li>
</ul>
<h2 id="data-integrity">5 Data Integrity</h2>
<p>This chapter explains how integrity constraints enforce business rules and prevent invalid data entry.</p>
<h3 id="introduction-to-data-integrity">1 Introduction to Data Integrity</h3>
<ul>
<li><strong>Data Integrity</strong>: Adherence to business rules defined by the database administrator or developer.</li>
<li><strong>Techniques for Guaranteeing Integrity</strong>:
<ul>
<li>Triggered stored procedures.</li>
<li>Stored procedures controlling data access.</li>
<li>Application code.</li>
<li>Integrity constraints (preferred method).</li>
</ul>
</li>
</ul>
<h4 id="advantages-of-integrity-constraints">Advantages of Integrity Constraints</h4>
<ul>
<li><strong>Declarative ease</strong>: Defined using SQL without additional programming.</li>
<li><strong>Centralized rules</strong>: Stored in the data dictionary and applied universally.</li>
<li><strong>Flexibility</strong>: Can be disabled during data loads.</li>
</ul>
<h3 id="types-of-integrity-constraints">2 Types of Integrity Constraints</h3>
<p>Constraints can be applied at the column or table level.</p>
<h4 id="not-null-constraints">NOT NULL Constraints</h4>
<ul>
<li>Prohibits null values in a column.</li>
</ul>
<h4 id="unique-constraints">Unique Constraints</h4>
<ul>
<li>Ensures all values in a column or set of columns are unique.</li>
<li>Allows null values unless combined with a <code>NOT NULL</code> constraint.</li>
</ul>
<h4 id="primary-key-constraints">Primary Key Constraints</h4>
<ul>
<li>Combines <code>NOT NULL</code> and unique constraints.</li>
<li>Uniquely identifies each row in a table.</li>
</ul>
<h4 id="foreign-key-constraints">Foreign Key Constraints</h4>
<ul>
<li>Enforces referential integrity between tables.</li>
<li><strong>Self-Referential Constraints</strong>: Foreign key references the same table.</li>
<li><strong>Nulls and Foreign Keys</strong>: Foreign keys can be null.</li>
<li><strong>Parent Key Modifications</strong>: Actions on deletion (e.g., <code>CASCADE</code>, <code>SET NULL</code>).</li>
</ul>
<h4 id="check-constraints">Check Constraints</h4>
<ul>
<li>Enforces a condition on column values (e.g., <code>salary &lt; 10000</code>).</li>
</ul>
<h3 id="states-of-integrity-constraints">3 States of Integrity Constraints</h3>
<p>Constraints can be enabled or disabled and validated or not validated.</p>
<h4 id="checks-for-modified-and-existing-data">Checks for Modified and Existing Data</h4>
<ul>
<li><strong>ENABLE VALIDATE</strong>: Checks all data (default).</li>
<li><strong>ENABLE NOVALIDATE</strong>: Checks new data only.</li>
<li><strong>DISABLE VALIDATE</strong>: Disables constraint but prevents modifications.</li>
<li><strong>DISABLE NOVALIDATE</strong>: Constraint is not enforced.</li>
</ul>
<h4 id="when-the-database-checks-constraints">When the Database Checks Constraints</h4>
<ul>
<li><strong>Nondeferrable Constraints</strong>: Checked immediately after each statement.</li>
<li><strong>Deferrable Constraints</strong>: Can be deferred until <code>COMMIT</code>.
<ul>
<li><strong>INITIALLY IMMEDIATE</strong>: Checked after each statement.</li>
<li><strong>INITIALLY DEFERRED</strong>: Checked at commit.</li>
</ul>
</li>
</ul>
<h4 id="examples-of-constraint-checking">Examples of Constraint Checking</h4>
<ul>
<li><strong>Insertion with Foreign Keys</strong>: Handling nulls or self-referential cases.</li>
<li><strong>Updates with Self-Referential Constraints</strong>: Checks performed after the entire statement executes.</li>
</ul>
<h2 id="application-data-usage">6 Application Data Usage</h2>
<p>This chapter explains the concept of schema annotations in Oracle Database, which are used to maintain additional property metadata for database objects.</p>
<h3 id="schema-annotations">1 Schema Annotations</h3>
<p>Schema annotations provide a mechanism to add custom properties to database metadata, such as tables, views, columns, indexes, and domains. These annotations are stored directly in the database and are used by applications to standardize behavior without being interpreted by the database itself.</p>
<h4 id="purpose-of-schema-annotations">Purpose of Schema Annotations</h4>
<ul>
<li>Maintain additional property metadata for database objects.</li>
<li>Standardize behavior across applications, modules, and microservices.</li>
<li>Avoid the need for custom repositories for usage metadata.</li>
</ul>
<h4 id="examples-of-column-level-annotations">Examples of Column-Level Annotations</h4>
<ul>
<li><strong>Display Label</strong>: Customize the display name of a column (e.g., “Salary” for <code>Employee_Salary</code>).</li>
<li><strong>Column Group</strong>: Group related columns (e.g., “Address” for street, city, and zip columns).</li>
<li><strong>Format Mask</strong>: Define display formats (e.g., <code>$99,999.99</code> for monetary values).</li>
<li><strong>Hide</strong>: Control column visibility in user interfaces (e.g., hide sensitive columns).</li>
<li><strong>Highlight</strong>: Indicate columns that should be visually emphasized.</li>
<li><strong>Allowed Operations</strong>: Specify permitted actions (e.g., sorting, grouping, displaying values).</li>
</ul>
<h4 id="examples-of-table-level-annotations">Examples of Table-Level Annotations</h4>
<ul>
<li><strong>Sensitive Information</strong>: Mark tables containing sensitive data.</li>
<li><strong>Display Name</strong>: Provide a user-friendly name for the table.</li>
<li><strong>Module Ownership</strong>: Identify which application module manages the table.</li>
</ul>
<h4 id="benefits-of-schema-annotations">Benefits of Schema Annotations</h4>
<ul>
<li><strong>Centralized Storage</strong>: Annotations are stored in the database dictionary, ensuring consistency.</li>
<li><strong>Lightweight and Declarative</strong>: Easy for developers to register and use.</li>
<li><strong>Standardization</strong>: Promotes uniform behavior across applications.</li>
</ul>
<h2 id="data-dictionary-and-dynamic-performance-views">7 Data Dictionary and Dynamic Performance Views</h2>
<h3 id="overview-of-the-data-dictionary">1 Overview of the Data Dictionary</h3>
<p>An important part of an Oracle database is its data dictionary, which is a read-only set of tables that provides administrative metadata about the database.</p>
<h4 id="contents-of-the-data-dictionary">Contents of the Data Dictionary</h4>
<ul>
<li><strong>Base tables</strong>: Store information about the database in a normalized and cryptic format. Only Oracle Database should write to or read these tables.</li>
<li><strong>Views</strong>: Decode base table data into useful information. Views are grouped in sets distinguished by prefixes:
<ul>
<li><strong>DBA_</strong>: For database administrators, showing all objects in the database.</li>
<li><strong>ALL_</strong>: For all users, showing objects to which the user has access.</li>
<li><strong>USER_</strong>: For all users, showing objects owned by the user.</li>
</ul>
</li>
</ul>
<h4 id="storage-of-the-data-dictionary">Storage of the Data Dictionary</h4>
<p>The data dictionary base tables are the first objects created in any Oracle database.</p>
<ul>
<li>All data dictionary tables and views are stored in the <code>SYSTEM</code> tablespace, which is always online when the database is open.</li>
</ul>
<h4 id="how-oracle-database-uses-the-data-dictionary">How Oracle Database Uses the Data Dictionary</h4>
<p>The <code>SYS</code> user account owns all base tables and user-accessible views.<br>
Oracle Database reads the data dictionary to validate schema objects and user access, and updates it continuously to reflect changes.</p>
<ul>
<li><strong>Public Synonyms</strong>: Oracle creates public synonyms for many data dictionary views for convenient access.</li>
<li><strong>Data Dictionary Cache</strong>: Frequently accessed data dictionary information is cached for performance.</li>
<li><strong>Other Programs</strong>: Oracle products may reference or extend the data dictionary.</li>
</ul>
<h4 id="the-dual-table">The DUAL Table</h4>
<p>A small table in the data dictionary used to return a known result (e.g., for calculations or system values), contains one column (<code>DUMMY</code>) and one row with the value <code>X</code>.</p>
<h3 id="overview-of-the-dynamic-performance-views">2 Overview of the Dynamic Performance Views</h3>
<p>Virtual tables that record current database activity, continuously updated while the database is in use. Their names begin with <code>V$</code>.</p>
<h4 id="contents-of-the-dynamic-performance-views">Contents of the Dynamic Performance Views</h4>
<ul>
<li><strong>Fixed views</strong>: Cannot be altered or removed by administrators. <code>SYS</code> owns the underlying tables (<code>V_$</code>), and public synonyms (<code>V$</code>) are created for user access.</li>
<li><strong>GV$ views</strong>: In Oracle RAC, these retrieve <code>V$</code> view information from all instances.</li>
</ul>
<h4 id="storage-of-the-dynamic-performance-views">Storage of the Dynamic Performance Views</h4>
<ul>
<li>Based on virtual tables built from memory structures, not conventional database tables.</li>
<li>Data is dynamic and read consistency is not guaranteed.</li>
<li>Availability depends on the database state (e.g., <code>V$DATAFILE</code> is only queryable after the database is mounted).</li>
</ul>
<h3 id="database-object-metadata">3 Database Object Metadata</h3>
<ul>
<li>The <code>DBMS_METADATA</code> package provides interfaces to extract complete definitions of database objects, expressed as XML or SQL DDL.</li>
<li>Offers both programmatic and simplified ad hoc querying interfaces.</li>
</ul>
<h1 id="part-ii-oracle-data-access">Part II: Oracle Data Access</h1>
<h2 id="sql">8 SQL</h2>
<p>This chapter provides an overview of the <strong>Structured Query Language (SQL)</strong> and how Oracle Database processes SQL statements.</p>
<h3 id="introduction-to-sql">1 Introduction to SQL</h3>
<p>SQL is the set-based, high-level declarative computer language used to access data in an Oracle database. It unifies tasks such as:</p>
<ul>
<li>Creating, replacing, altering, and dropping objects.</li>
<li>Inserting, updating, and deleting table rows.</li>
<li>Querying data.</li>
<li>Controlling access to the database and its objects.</li>
<li>Guaranteeing database consistency and integrity.</li>
</ul>
<h4 id="sql-data-access">SQL Data Access</h4>
<ul>
<li><strong>Declarative languages</strong>: Nonprocedural, describe what should be done (e.g., SQL).</li>
<li><strong>Procedural languages</strong>: Describe how things should be done (e.g., C++, Java).</li>
</ul>
<h4 id="sql-standards">SQL Standards</h4>
<p>Oracle follows industry-accepted standards (ANSI/ISO) and extends SQL with additional features.</p>
<h3 id="overview-of-sql-statements">2 Overview of SQL Statements</h3>
<p>SQL statements are categorized as follows:</p>
<ul>
<li><strong>Data Definition Language (DDL) Statements</strong>: Define, alter, or drop schema objects (e.g., <code>CREATE</code>, <code>ALTER</code>, <code>DROP</code>).</li>
<li><strong>Data Manipulation Language (DML) Statements</strong>: Query or manipulate data (e.g., <code>SELECT</code>, <code>INSERT</code>, <code>UPDATE</code>, <code>DELETE</code>).</li>
<li><strong>Transaction Control Statements</strong>: Manage transactions (e.g., <code>COMMIT</code>, <code>ROLLBACK</code>, <code>SAVEPOINT</code>).</li>
<li><strong>Session Control Statements</strong>: Dynamically manage user session properties (e.g., <code>ALTER SESSION</code>, <code>SET ROLE</code>).</li>
<li><strong>System Control Statement</strong>: Change database instance properties (e.g., <code>ALTER SYSTEM</code>).</li>
<li><strong>Embedded SQL Statements</strong>: Incorporate SQL within procedural language programs (e.g., <code>DECLARE CURSOR</code>, <code>FETCH</code>).</li>
</ul>
<h4 id="data-definition-language-ddl-statements">Data Definition Language (DDL) Statements</h4>
<p>Data definition language (DLL) statements define, structurally change, and drop schema objects.</p>
<ul>
<li>Examples: <code>CREATE TABLE</code>, <code>ALTER TABLE</code>, <code>DROP TABLE</code>, <code>GRANT</code>, <code>REVOKE</code>.</li>
<li>Implicitly commit transactions before and after execution.</li>
</ul>
<h4 id="data-manipulation-language-dml-statements">Data Manipulation Language (DML) Statements</h4>
<p>Data manipulation language (DML) statements query or manipulate data in existing schema objects.</p>
<ul>
<li>Examples: <code>SELECT</code>, <code>INSERT</code>, <code>UPDATE</code>, <code>DELETE</code>, <code>MERGE</code>.</li>
<li>Do not implicitly commit transactions.</li>
</ul>
<h5 id="select-statements">SELECT Statements</h5>
<ul>
<li>Retrieve data from tables or views.</li>
<li>Keywords: <code>SELECT</code>, <code>FROM</code>, <code>WHERE</code>, <code>ORDER BY</code>.</li>
</ul>
<h5 id="joins">Joins</h5>
<ul>
<li>Combine rows from multiple tables.</li>
<li>Types: Inner joins, outer joins (left, right, full), Cartesian products.</li>
</ul>
<h5 id="subqueries">Subqueries</h5>
<ul>
<li>Nested <code>SELECT</code> statements within another SQL statement.</li>
</ul>
<h4 id="transaction-control-statements">Transaction Control Statements</h4>
<p>Transaction control statements manage the changes made by DML statements and group DML statements into transactions.</p>
<ul>
<li>Examples: <code>COMMIT</code>, <code>ROLLBACK</code>, <code>SAVEPOINT</code>, <code>SET TRANSACTION</code>.</li>
</ul>
<h4 id="session-control-statements">Session Control Statements</h4>
<p>A session is a logical entity in the database instance memory that represents the state of a current user login to a database. A session lasts from the time the user is authenticated by the database until the user disconnects or exits the database application.</p>
<ul>
<li>Examples: <code>ALTER SESSION</code>, <code>SET ROLE</code>.</li>
</ul>
<h4 id="system-control-statement">System Control Statement</h4>
<p>A system control statement changes the properties of the database instance. The only system control statement is <code>ALTER SYSTEM</code>. It enables you to change settings such as the minimum number of shared servers, terminate a session, and perform other system-level tasks.</p>
<h4 id="embedded-sql-statements">Embedded SQL Statements</h4>
<ul>
<li>Used in procedural languages (e.g., <code>DECLARE CURSOR</code>, <code>FETCH</code>).</li>
</ul>
<h3 id="overview-of-the-optimizer">3 Overview of the Optimizer</h3>
<p>The optimizer determines the most efficient way to execute SQL statements.</p>
<h4 id="use-of-the-optimizer">Use of the Optimizer</h4>
<ul>
<li>Generates execution plans based on query conditions, access paths, and statistics.</li>
<li>Optimizer goals: Total throughput (<code>ALL_ROWS</code>) or initial response time (<code>FIRST_ROWS</code>).</li>
</ul>
<h4 id="optimizer-components">Optimizer Components</h4>
<ol>
<li><strong>Query Transformer</strong>: Rewrites queries for better execution plans.</li>
<li><strong>Estimator</strong>: Calculates selectivity, cardinality, and cost.</li>
<li><strong>Plan Generator</strong>: Chooses the lowest-cost execution plan.</li>
</ol>
<h4 id="access-paths">Access Paths</h4>
<p>Techniques to retrieve data:</p>
<ul>
<li><strong>Full table scans</strong>: This type of scan reads all rows from a table and filters out those that do not meet the selection criteria.</li>
<li><strong>Rowid scans</strong>: The rowid of a row specifies the data file and data block containing the row and the location of the row in that block. The database first obtains the rowids of the selected rows, either from the statement WHERE clause or through an index scan, and then locates each selected row based on its rowid.</li>
<li><strong>Index scans</strong>: This scan searches an index for the indexed column values accessed by the SQL statement. If the statement accesses only columns of the index, then Oracle Database reads the indexed column values directly from the index.</li>
<li><strong>Cluster scans</strong>: A cluster scan retrieves data from a table stored in an indexed table cluster, where all rows with the same cluster key value are stored in the same data block. The database first obtains the rowid of a selected row by scanning the cluster index. Oracle Database locates the rows based on this rowid.</li>
<li><strong>Hash scans</strong>: A hash scan locates rows in a hash cluster, where all rows with the same hash value are stored in the same data block. The database first obtains the hash value by applying a hash function to a cluster key value specified by the statement. Oracle Database then scans the data blocks containing rows with this hash value.</li>
</ul>
<h4 id="optimizer-statistics">Optimizer Statistics</h4>
<p>The optimizer statistics are a collection of data that describe details about the database and the objects in the database. The statistics provide a statistically correct picture of data storage and distribution usable by the optimizer when evaluating access paths.</p>
<ul>
<li>Optimizer statistics include: Tables, Columns, Indexes, System Statistics.</li>
<li>Gathered automatically or manually using <code>DBMS_STATS</code>.</li>
</ul>
<h4 id="optimizer-hints">Optimizer Hints</h4>
<p>A hint is a comment in a SQL statement that acts as an instruction to the optimizer.</p>
<ul>
<li>Instructions to the optimizer (e.g., <code>/*+ FIRST_ROWS(25) */</code>).</li>
</ul>
<h3 id="overview-of-sql-processing">4 Overview of SQL Processing</h3>
<p>Stages of SQL statement processing:</p>
<ol>
<li><strong>SQL Parsing</strong>: The first stage of SQL processing is SQL parsing. This stage involves separating the pieces of a SQL statement into a data structure that can be processed by other routines. It contains syntax, semantic, and shared pool checks.</li>
<li><strong>SQL Optimization</strong>: Query optimization is the process of choosing the most efficient means of executing a SQL statement.</li>
<li><strong>SQL Row Source Generation</strong>: The row source generator is a software that receives the optimal execution plan from the optimizer and produces an iterative plan, called the query plan, that is usable by the rest of the database.</li>
<li><strong>SQL Execution</strong>: During execution, the SQL engine executes each row source in the tree produced by the row source generator. This is the only mandatory step in DML processing.</li>
</ol>
<h4 id="differences-between-dml-and-ddl-processing">Differences Between DML and DDL Processing</h4>
<ul>
<li>DDL statements are not optimized; they are parsed and executed directly.</li>
<li>DML statements involve query optimization and execution plans.</li>
</ul>
<h2 id="server-side-programming-plsql-and-java">9 Server-Side Programming: PL/SQL and Java</h2>
<h3 id="introduction-to-server-side-programming">1 Introduction to Server-Side Programming</h3>
<ul>
<li><strong>Definition</strong>: Explains how PL/SQL or Java programs stored in the database can use SQL.</li>
<li><strong>Key Topics</strong>:
<ul>
<li>Introduction to Server-Side Programming</li>
<li>Overview of PL/SQL</li>
<li>Overview of Java in Oracle Database</li>
<li>Overview of Triggers</li>
</ul>
</li>
</ul>
<h4 id="key-points">Key Points</h4>
<ul>
<li><strong>Nonprocedural vs. Procedural Languages</strong>: SQL is nonprocedural (specifies data but not operations), while procedural languages (like PL/SQL or Java) use control structures.</li>
<li><strong>Approaches</strong>:
<ul>
<li><strong>Client-Side Programming</strong>: Embed SQL in applications (e.g., C, C++, Java).</li>
<li><strong>Server-Side Programming</strong>: Develop logic in the database (e.g., stored subprograms, triggers).</li>
</ul>
</li>
<li><strong>Benefits of Server-Side Programming</strong>:
<ul>
<li>Centralized processing improves scalability.</li>
<li>Reduced network traffic.</li>
<li>Reusable code.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-plsql">2 Overview of PL/SQL</h3>
<ul>
<li><strong>Definition</strong>: A server-side, stored procedural language integrated with SQL.</li>
<li><strong>PL/SQL Units</strong>:
<ul>
<li><strong>Subprograms</strong>: Named blocks (procedures/functions) stored in the database.</li>
<li><strong>Anonymous Blocks</strong>: Unnamed, non-persistent blocks.</li>
<li><strong>Packages</strong>: Groups of related subprograms, variables, and cursors.</li>
</ul>
</li>
</ul>
<h4 id="plsql-subprograms">PL/SQL Subprograms</h4>
<ul>
<li><strong>Types</strong>: Procedures (no return value) and functions (return a value).</li>
<li><strong>Advantages</strong>:
<ul>
<li>Improved performance (compiled form available).</li>
<li>Memory efficiency (shared memory).</li>
<li>Code reusability and integrity.</li>
<li>Security (definer’s/invoker’s rights).</li>
</ul>
</li>
<li><strong>Creation</strong>: The database stores subprograms in the data dictionary as schema objects. A subprogram has a specification, which includes descriptions of any parameters, and a body.</li>
</ul>
<h3 id="plsql-packages">PL/SQL Packages</h3>
<ul>
<li><strong>Definition</strong>: Groups related subprograms, variables, and cursors.</li>
<li><strong>Advantages</strong>:
<ul>
<li>Encapsulation and data security.</li>
<li>Better performance (loaded in memory once).</li>
</ul>
</li>
<li><strong>Creation</strong>: Split into specification (public constructs) and body (implementation).</li>
</ul>
<h4 id="plsql-anonymous-blocks">PL/SQL Anonymous Blocks</h4>
<ul>
<li><strong>Definition</strong>: Unnamed, non-persistent unit used for ad-hoc tasks.</li>
<li><strong>Differences from Subprograms</strong>:
<ul>
<li>Not stored in the database.</li>
<li>No reusability or parameter support.</li>
</ul>
</li>
</ul>
<h4 id="plsql-language-constructs">PL/SQL Language Constructs</h4>
<ul>
<li>Includes variables, constants, cursors (A handle or name for a private SQL area in the PGA), exceptions, and dynamic SQL (statements whose complete text is not known until run time).</li>
</ul>
<h4 id="plsql-collections-and-records">PL/SQL Collections and Records</h4>
<ul>
<li><strong>Collections</strong>: Ordered groups of elements (e.g., arrays, nested tables).</li>
<li><strong>Records</strong>: Composite variables storing different data types.</li>
</ul>
<h4 id="how-plsql-runs">How PL/SQL Runs</h4>
<ul>
<li><strong>Modes</strong>:
<ul>
<li>Interpreted execution (bytecode).</li>
<li>Native execution (direct to object code).</li>
</ul>
</li>
<li><strong>PL/SQL Engine</strong>: Processes PL/SQL units within Oracle Database.</li>
</ul>
<hr>
<h3 id="overview-of-java-in-oracle-database">3 Overview of Java in Oracle Database</h3>
<ul>
<li><strong>Features</strong>:
<ul>
<li>Platform independence (JVM).</li>
<li>Automated memory management.</li>
<li>Strong typing.</li>
</ul>
</li>
</ul>
<h4 id="java-virtual-machine-jvm">Java Virtual Machine (JVM)</h4>
<ul>
<li><strong>Oracle JVM</strong>: Standard, Java-compatible environment embedded in the database.</li>
<li><strong>Components</strong>: Runs in the same process space as the database kernel.</li>
</ul>
<h4 id="java-programming-environment">Java Programming Environment</h4>
<ul>
<li><strong>Java Stored Procedures</strong>: Equivalent to PL/SQL subprograms.</li>
<li><strong>Integration with PL/SQL</strong>: Call Java from PL/SQL and vice versa.</li>
<li><strong>JDBC Drivers</strong>:
<ul>
<li>Thin driver (pure Java).</li>
<li>OCI driver (Oracle-specific native code).</li>
<li>Server-side internal driver (local data access).</li>
</ul>
</li>
</ul>
<h4 id="sqlj">SQLJ</h4>
<ul>
<li><strong>Definition</strong>: ANSI standard for embedding SQL in Java.</li>
<li><strong>Usage</strong>: Translates embedded SQL to JDBC-based Java code.</li>
</ul>
<hr>
<h3 id="overview-of-triggers">4 Overview of Triggers</h3>
<ul>
<li><strong>Definition</strong>: Compiled stored program units (PL/SQL or Java) invoked automatically.</li>
<li><strong>Triggering Events</strong>:
<ul>
<li>DML statements (INSERT, UPDATE, DELETE).</li>
<li>DDL statements.</li>
<li>Database events (login, shutdown).</li>
</ul>
</li>
</ul>
<h4 id="advantages-of-triggers">Advantages of Triggers</h4>
<ul>
<li>Enforce business rules.</li>
<li>Automate derived values.</li>
<li>Provide auditing.</li>
</ul>
<h4 id="types-of-triggers">Types of Triggers</h4>
<ul>
<li><strong>Row Triggers</strong>: Fired per affected row.</li>
<li><strong>Statement Triggers</strong>: Fired once per statement, regardless of the number of rows affected by the triggering statement.</li>
<li><strong>INSTEAD OF Triggers</strong>: Modify views indirectly. These triggers are useful for transparently modifying views that cannot be modified directly through DML statements.</li>
<li><strong>Event Triggers</strong>: You can use triggers to publish information about database events to subscribers. Event triggers are divided into the following categories:
<ul>
<li>A <strong>system event trigger</strong> can be caused by events such as database instance startup and shutdown or error messages.</li>
<li>A <strong>user event trigger</strong> is fired because of events related to user logon and logoff, DDL statements, and DML statements.</li>
</ul>
</li>
</ul>
<h4 id="timing-for-triggers">Timing for Triggers</h4>
<ul>
<li><strong>BEFORE/AFTER</strong>: Enhance security or log actions.</li>
<li><strong>Compound Triggers</strong>: Fire at multiple timing points. Compound triggers help program an approach in which the actions that you implement for various timing points share common data.</li>
</ul>
<h4 id="creation-and-execution">Creation and Execution</h4>
<ul>
<li><strong>Syntax</strong>: <code>CREATE TRIGGER</code> with event, restriction, and action.</li>
<li><strong>Example</strong>: Trigger to update order item counts.</li>
</ul>
<h4 id="storage-of-triggers">Storage of Triggers</h4>
<ul>
<li>Stored in compiled form in the database.</li>
<li>Java triggers reference separately compiled Java code.</li>
</ul>
<h1 id="part-iii-oracle-transaction-management">Part III: Oracle Transaction Management</h1>
<p>Transaction management ensures data concurrency and consistency in a multiuser database environment.</p>
<ul>
<li><strong>Chapters</strong>:
<ul>
<li>Data Concurrency and Consistency</li>
<li>Transactions</li>
</ul>
</li>
</ul>
<hr>
<h2 id="data-concurrency-and-consistency">10 Data Concurrency and Consistency</h2>
<h3 id="introduction-to-data-concurrency-and-consistency">1 Introduction to Data Concurrency and Consistency</h3>
<ul>
<li><strong>Single-User vs. Multiuser Databases</strong>: In a single-user database, modifications are straightforward. In a multiuser database, concurrent transactions must produce consistent results.</li>
<li><strong>Requirements</strong>:
<ul>
<li><strong>Data Concurrency</strong>: Multiple users can access data simultaneously.</li>
<li><strong>Data Consistency</strong>: Each user sees a consistent view of data, including their own changes and committed changes by others.</li>
</ul>
</li>
<li><strong>Serializability</strong>: A model where transactions appear to execute sequentially, ensuring isolation. However, perfect isolation can impact performance.</li>
</ul>
<h4 id="multiversion-read-consistency">Multiversion Read Consistency</h4>
<ul>
<li><strong>Definition</strong>: Oracle Database maintains multiple versions of data to provide consistent views.</li>
<li><strong>Features</strong>:
<ul>
<li><strong>Read-Consistent Queries</strong>: Data returned is committed and consistent for a specific point in time.</li>
<li><strong>Nonblocking Queries</strong>: Readers and writers do not block each other.</li>
<li><strong>No Dirty Reads</strong>: Oracle never allows reading uncommitted data.</li>
</ul>
</li>
<li><strong>Levels</strong>:
<ul>
<li><strong>Statement-Level Read Consistency</strong>: Ensures a single query sees data consistent at the time the query began.</li>
<li><strong>Transaction-Level Read Consistency</strong>: Extends consistency to all queries in a transaction.</li>
</ul>
</li>
<li><strong>Undo Segments</strong>: Used to reconstruct previous versions of data for read consistency.</li>
</ul>
<h4 id="locking-mechanisms">Locking Mechanisms</h4>
<ul>
<li><strong>Purpose</strong>: Prevent destructive interactions between concurrent transactions.</li>
<li><strong>Types</strong>:
<ul>
<li><strong>Automatic Locks</strong>: Acquired by Oracle on behalf of transactions.</li>
<li><strong>Manual Locks</strong>: Override default locking mechanisms.</li>
<li><strong>User-Defined Locks</strong>: Custom locks for specific applications.</li>
</ul>
</li>
</ul>
<h4 id="ansiiso-transaction-isolation-levels">ANSI/ISO Transaction Isolation Levels</h4>
<ul>
<li><strong>Preventable Phenomena</strong>:
<ul>
<li><strong>Dirty Reads</strong>: Reading uncommitted data.</li>
<li><strong>Nonrepeatable Reads</strong>: Rereading data to find it modified or deleted.</li>
<li><strong>Phantom Reads</strong>: Rerunning a query to find new rows matching the condition.</li>
</ul>
</li>
<li><strong>Isolation Levels</strong>:
<ul>
<li><strong>Read Uncommitted</strong>: Allows all phenomena.</li>
<li><strong>Read Committed</strong>: Prevents dirty reads (Oracle’s default).</li>
<li><strong>Repeatable Read</strong>: Prevents dirty and nonrepeatable reads.</li>
<li><strong>Serializable</strong>: Prevents all phenomena.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-oracle-database-transaction-isolation-levels">2 Overview of Oracle Database Transaction Isolation Levels</h3>
<h4 id="read-committed-isolation-level">Read Committed Isolation Level</h4>
<ul>
<li><strong>Default Level</strong>: Queries see only data committed before the query began.</li>
<li><strong>Features</strong>:
<ul>
<li><strong>Conflicting Writes</strong>: Transactions wait for blocking transactions to release locks.</li>
<li><strong>Lost Updates</strong>: A common issue where one transaction’s update is overwritten by another.</li>
</ul>
</li>
</ul>
<h4 id="serializable-isolation-level">Serializable Isolation Level</h4>
<ul>
<li><strong>Definition</strong>: Transactions see only changes committed when the transaction began and their own changes.</li>
<li><strong>Use Cases</strong>: Large databases with short transactions or long-running read-only transactions.</li>
<li><strong>Error Handling</strong>: <code>ORA-08177</code> occurs if a transaction tries to modify data changed by another committed transaction.</li>
</ul>
<h4 id="read-only-isolation-level">Read-Only Isolation Level</h4>
<ul>
<li><strong>Similar to Serializable</strong>: No modifications allowed unless the user is <code>SYS</code>.</li>
<li><strong>Use Cases</strong>: Generating reports requiring consistent data.</li>
<li><strong>Undo Retention</strong>: Ensures long-running reports avoid <code>snapshot too old</code> errors.</li>
</ul>
<h3 id="overview-of-the-oracle-database-locking-mechanism">3 Overview of the Oracle Database Locking Mechanism</h3>
<h4 id="summary-of-locking-behavior">Summary of Locking Behavior</h4>
<ul>
<li><strong>Types</strong>:
<ul>
<li><strong>Exclusive Locks</strong>: Prevent sharing (e.g., row locks for updates).</li>
<li><strong>Share Locks</strong>: Allow sharing (e.g., for read operations).</li>
</ul>
</li>
<li><strong>Rules</strong>:
<ul>
<li>Writers block concurrent writers of the same row.</li>
<li>Readers never block writers, and writers never block readers.</li>
</ul>
</li>
</ul>
<h4 id="use-of-locks">Use of Locks</h4>
<ul>
<li><strong>Purpose</strong>: Ensure consistency and integrity in multiuser environments.</li>
<li><strong>Example</strong>: Prevents lost updates by locking rows during modifications.</li>
</ul>
<h4 id="lock-modes">Lock Modes</h4>
<ul>
<li><strong>Exclusive Mode</strong>: Prevents sharing (e.g., row locks for updates).</li>
<li><strong>Share Mode</strong>: Allows sharing (e.g., for read operations).</li>
</ul>
<h4 id="lock-conversion-and-escalation">Lock Conversion and Escalation</h4>
<ul>
<li><strong>Conversion</strong>: Automatically increases lock restrictiveness (e.g., row share to row exclusive).</li>
<li><strong>Escalation</strong>: Oracle does not escalate locks (e.g., row locks to table locks), avoiding deadlocks.</li>
</ul>
<h4 id="lock-duration">Lock Duration</h4>
<ul>
<li><strong>Release</strong>: Locks are released when the transaction ends (commit or rollback).</li>
<li><strong>Exception</strong>: Table locks for unindexed foreign keys are released after the statement.</li>
</ul>
<h4 id="locks-and-deadlocks">Locks and Deadlocks</h4>
<ul>
<li><strong>Definition</strong>: Two or more transactions waiting for each other’s locks.</li>
<li><strong>Resolution</strong>: Oracle detects and resolves deadlocks by rolling back one statement.</li>
</ul>
<h3 id="overview-of-automatic-locks">4 Overview of Automatic Locks</h3>
<h4 id="dml-locks">DML Locks</h4>
<ul>
<li><strong>Purpose</strong>: Protect data integrity during DML operations.</li>
<li><strong>Types</strong>:
<ul>
<li><strong>Row Locks (TX)</strong>: Lock single rows during modifications.</li>
<li><strong>Table Locks ™</strong>: Lock tables during DML operations (e.g., <code>INSERT</code>, <code>UPDATE</code>).</li>
</ul>
</li>
<li><strong>Modes</strong>:
<ul>
<li><strong>Row Share (RS)</strong>: Least restrictive, allows concurrent updates.</li>
<li><strong>Row Exclusive (RX)</strong>: Allows concurrent queries but not DDL.</li>
<li><strong>Exclusive (X)</strong>: Most restrictive, prohibits all concurrent operations.</li>
</ul>
</li>
</ul>
<h4 id="ddl-locks">DDL Locks</h4>
<ul>
<li><strong>Purpose</strong>: Protect schema object definitions during DDL operations.</li>
<li><strong>Types</strong>:
<ul>
<li><strong>Exclusive DDL Locks</strong>: Prevent other DDL or DML locks.</li>
<li><strong>Share DDL Locks</strong>: Allow concurrent similar DDL operations.</li>
<li><strong>Breakable Parse Locks</strong>: Held during SQL parsing, invalidated if objects change.</li>
</ul>
</li>
</ul>
<h4 id="system-locks">System Locks</h4>
<ul>
<li><strong>Purpose</strong>: Protect internal database structures.</li>
<li><strong>Types</strong>:
<ul>
<li><strong>Latches</strong>: Low-level serialization for shared memory structures.</li>
<li><strong>Mutexes</strong>: Protect single objects from corruption.</li>
<li><strong>Internal Locks</strong>: Higher-level locks for dictionary caches, files, and tablespaces.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-manual-data-locks">5 Overview of Manual Data Locks</h3>
<ul>
<li><strong>Purpose</strong>: Override default locking for specific needs (e.g., transaction-level consistency).</li>
<li><strong>Methods</strong>:
<ul>
<li><code>SET TRANSACTION ISOLATION LEVEL</code></li>
<li><code>LOCK TABLE</code></li>
<li><code>SELECT ... FOR UPDATE</code></li>
</ul>
</li>
<li><strong>Considerations</strong>: Ensure data integrity, concurrency, and deadlock avoidance.</li>
</ul>
<h3 id="overview-of-user-defined-locks">6 Overview of User-Defined Locks</h3>
<ul>
<li><strong>Purpose</strong>: Custom locks for application-specific needs.</li>
<li><strong>Implementation</strong>: Use the <code>DBMS_LOCK</code> package to create, modify, and release locks.</li>
<li><strong>Naming</strong>: User locks are prefixed with <code>UL</code> to avoid conflicts with Oracle locks.</li>
</ul>
<h2 id="transactions">11 Transactions</h2>
<h3 id="introduction-to-transactions">1 Introduction to Transactions</h3>
<ul>
<li><strong>Definition</strong>: A transaction is a logical, atomic unit of work containing one or more SQL statements, ensuring all changes are committed or rolled back as a unit.</li>
<li><strong>ACID Properties</strong>:
<ul>
<li><strong>Atomicity</strong>: All tasks complete or none do (no partial transactions).</li>
<li><strong>Consistency</strong>: Transitions the database from one valid state to another.</li>
<li><strong>Isolation</strong>: Changes are invisible to others until committed.</li>
<li><strong>Durability</strong>: Committed changes are permanent.</li>
</ul>
</li>
<li><strong>Key Concepts</strong>:
<ul>
<li><strong>Transaction ID</strong>: Unique identifier assigned by Oracle.</li>
<li><strong>Statement-Level Atomicity</strong>: Each SQL statement succeeds or fails entirely.</li>
<li><strong>System Change Numbers (SCNs)</strong>: Logical timestamps ordering database events.</li>
</ul>
</li>
</ul>
<h4 id="structure-of-a-transaction">Structure of a Transaction</h4>
<ul>
<li><strong>Beginning</strong>: Starts with the first executable SQL statement (DML/DDL).</li>
<li><strong>End</strong>: Triggered by:
<ul>
<li>Explicit <code>COMMIT</code> or <code>ROLLBACK</code>.</li>
<li>DDL statements (implicit commit).</li>
<li>Normal exit from tools (implicit commit).</li>
<li>Abnormal termination (implicit rollback).</li>
</ul>
</li>
</ul>
<h4 id="system-change-numbers-scns">System Change Numbers (SCNs)</h4>
<ul>
<li>Logical, internal timestamps for ordering events.</li>
<li>Used in recovery, transaction commits, and ensuring data consistency: Oracle Database uses SCNs to mark the SCN before which all changes are known to be on disk so that recovery avoids applying unnecessary redo. The database also uses SCNs to mark the point at which no redo exists for a set of data so that recovery can stop.</li>
</ul>
<h3 id="overview-of-transaction-control">2 Overview of Transaction Control</h3>
<ul>
<li><strong>Purpose</strong>: Manage DML changes and group them into transactions.</li>
<li><strong>Key Statements</strong>:
<ul>
<li><code>COMMIT</code>: Makes changes permanent, releases locks.</li>
<li><code>ROLLBACK</code>: Undoes changes since last commit/savepoint.</li>
<li><code>SAVEPOINT</code>: Creates intermediate markers for partial rollback.</li>
</ul>
</li>
</ul>
<h4 id="transaction-names">Transaction Names</h4>
<ul>
<li>Optional user-defined tags (e.g., <code>sal_update</code>) for monitoring.</li>
<li>Visible in tools like Oracle Enterprise Manager.</li>
</ul>
<h4 id="active-transactions">Active Transactions</h4>
<ul>
<li>Transactions that have started but not yet committed/rolled back.</li>
<li>Temporary changes in SGA until completion.</li>
</ul>
<h4 id="savepoints">Savepoints</h4>
<ul>
<li>Intermediate markers within transactions.</li>
<li><strong>Rollback to Savepoint</strong>: Undoes changes after the savepoint but keeps the transaction active.</li>
</ul>
<h4 id="rollback-of-transactions">Rollback of Transactions</h4>
<ul>
<li>Undoes all changes, releases locks, and ends the transaction.</li>
<li>Uses undo segments to reverse operations.</li>
</ul>
<h4 id="commits-of-transactions">Commits of Transactions</h4>
<ul>
<li><strong>Actions</strong>:
<ol>
<li>Generates an SCN.</li>
<li>Writes redo logs via LGWR.</li>
<li>Releases locks.</li>
<li>Performs commit cleanout (removes lock-related info from blocks).</li>
</ol>
</li>
<li><strong>Performance</strong>: Fast, regardless of transaction size.</li>
</ul>
<h3 id="overview-of-transaction-guard">3 Overview of Transaction Guard</h3>
<ul>
<li><strong>Purpose</strong>: Provides transaction idempotence (ensures at-most-once execution) after recoverable errors (e.g., network failures).</li>
<li><strong>Key Features</strong>:
<ul>
<li><strong>Logical Transaction ID</strong>: Globally unique identifier for tracking transaction outcomes.</li>
<li><strong>API Support</strong>: JDBC, OCI, OCCI, <a href="http://ODP.Net">ODP.Net</a>.</li>
</ul>
</li>
<li><strong>Benefits</strong>: Prevents duplicate transactions (e.g., double charges in e-commerce).</li>
</ul>
<h4 id="how-transaction-guard-works">How Transaction Guard Works</h4>
<ul>
<li><strong>Lost Commit Messages</strong>: Solves ambiguity after communication failures.</li>
<li><strong>Logical Transaction ID</strong>: Persists commit outcomes for retrieval post-failure.</li>
</ul>
<h4 id="transaction-guard-example">Transaction Guard Example</h4>
<ul>
<li>Uses logical transaction IDs to confirm commit status, enabling safe retries or user notifications.</li>
</ul>
<h3 id="overview-of-application-continuity">4 Overview of Application Continuity</h3>
<ul>
<li><strong>Purpose</strong>: Masks outages by replaying incomplete requests after failures.</li>
<li><strong>Phases</strong>:
<ol>
<li><strong>Runtime</strong>: Identifies replayable requests.</li>
<li><strong>Reconnection</strong>: Re-establishes connection post-failure.</li>
<li><strong>Replay</strong>: Re-executes requests from point of failure.</li>
</ol>
</li>
</ul>
<h4 id="benefits-2">Benefits</h4>
<ul>
<li><strong>Use Case</strong>: Restores session state (transactions, cursors, variables) after disruptions.</li>
<li><strong>Planned Maintenance</strong>: Enables session migration without errors.</li>
</ul>
<h4 id="architecture">Architecture</h4>
<p>The key components of Application Continuity are runtime, reconnection, and replay.</p>
<ul>
<li>Integrates with Transaction Guard to ensure idempotence during replays.</li>
</ul>
<h3 id="overview-of-autonomous-transactions">5 Overview of Autonomous Transactions</h3>
<ul>
<li><strong>Definition</strong>: Independent transactions called from another (main) transaction.</li>
<li><strong>Characteristics</strong>:
<ul>
<li>Isolated from the main transaction (no shared locks/resources).</li>
<li>Commits independently (changes visible immediately).</li>
<li>Useful for logging or secondary operations (e.g., audit trails).</li>
</ul>
</li>
</ul>
<h4 id="example">Example</h4>
<ul>
<li>PL/SQL routines marked with <code>PRAGMA AUTONOMOUS_TRANSACTION</code>.</li>
<li>Control flow suspends the main transaction during autonomous execution.</li>
</ul>
<h3 id="overview-of-autonomous-transaction">7 Overview of Autonomous Transaction</h3>
<p>An autonomous transaction is an independent transaction that can be called from another transaction, which is the main transaction. You can suspend the calling transaction, perform SQL operations and commit or undo them in the autonomous transaction, and then resume the calling transaction.<br>
Autonomous transactions are useful for actions that must be performed independently, regardless of whether the calling transaction commits or rolls back. For example, in a stock purchase transaction, you want to commit customer data regardless of whether the overall stock purchase goes through. Additionally, you want to log error messages to a debug table even if the overall transaction rolls back.</p>
<h3 id="overview-of-distributed-transactions">6 Overview of Distributed Transactions</h3>
<ul>
<li><strong>Definition</strong>: Transactions spanning multiple databases via database links.</li>
<li><strong>Challenge</strong>: Coordinating commits/rollbacks across nodes.</li>
</ul>
<h4 id="two-phase-commit">Two-Phase Commit</h4>
<p>The two-phase commit mechanism guarantees that all databases participating in a distributed transaction either all commit or all undo the statements in the transaction. The mechanism also protects implicit DML performed by integrity constraints, remote procedure calls, and triggers.</p>
<ol>
<li><strong>Prepare Phase</strong>: Coordinator checks if all nodes can commit.</li>
<li><strong>Commit Phase</strong>: If all agree, changes are finalized; otherwise, rolled back.</li>
</ol>
<h4 id="in-doubt-transactions">In-Doubt Transactions</h4>
<p>An in-doubt distributed transaction occurs when a two-phase commit was interrupted by any type of system or network failure.</p>
<ul>
<li><strong>Resolution</strong>:
<ul>
<li>Automated by the Recoverer (RECO) process.</li>
<li>Manual intervention for long-term failures.</li>
</ul>
</li>
</ul>
<h1 id="part-iv-oracle-database-storage-structures">Part IV: Oracle Database Storage Structures</h1>
<p>This part describes the basic structural architecture of the Oracle database, including logical and physical storage structures.</p>
<h2 id="physical-storage-structures">12 Physical Storage Structures</h2>
<p>The physical database structures of an Oracle database are viewable at the operating system level.</p>
<h3 id="introduction-to-physical-storage-structures">1 Introduction to Physical Storage Structures</h3>
<ul>
<li>One characteristic of an RDBMS is the independence of logical data structures (tables, views, indexes) from physical storage structures.</li>
<li>Physical and logical structures are separate, allowing management of physical storage without affecting logical access.</li>
<li>An Oracle database is a set of files storing data persistently, generated by the <code>CREATE DATABASE</code> statement:
<ul>
<li><strong>Data files and temp files</strong>: Store data in Oracle proprietary format.</li>
<li><strong>Control files</strong>: Track physical components of the database.</li>
<li><strong>Online redo log files</strong>: Record changes made to data.</li>
</ul>
</li>
</ul>
<h4 id="mechanisms-for-storing-database-files">Mechanisms for Storing Database Files</h4>
<ul>
<li><strong>Oracle Automatic Storage Management (Oracle ASM)</strong>:
<ul>
<li>High-performance, database-exclusive file system.</li>
<li>Manages disk space and I/O load automatically.</li>
</ul>
</li>
<li><strong>Operating System File System</strong>: Traditional file storage managed by the OS.</li>
<li><strong>Cluster File System</strong>: Distributed file system for high availability in clustered environments.</li>
</ul>
<h4 id="oracle-asm-storage-components">Oracle ASM Storage Components</h4>
<ul>
<li><strong>Oracle ASM Disks</strong>: Storage devices provisioned to disk groups.</li>
<li><strong>Oracle ASM Disk Groups</strong>: Logical units managing disks.</li>
<li><strong>Oracle ASM Files</strong>: Database files stored in disk groups.</li>
<li><strong>Oracle ASM Extents and Allocation Units</strong>: Fundamental units for space allocation.</li>
</ul>
<h4 id="oracle-asm-instances">Oracle ASM Instances</h4>
<ul>
<li>Special Oracle instances managing ASM disks.</li>
<li>Provide metadata and layout information to database instances.</li>
</ul>
<h4 id="oracle-managed-files-and-user-managed-files">Oracle Managed Files and User-Managed Files</h4>
<ul>
<li><strong>Oracle Managed Files</strong>: Simplifies file management by automating naming and allocation.</li>
<li><strong>User-Managed Files</strong>: Direct management of OS files by administrators.</li>
</ul>
<h3 id="overview-of-data-files">2 Overview of Data Files</h3>
<ul>
<li><strong>Use of Data Files</strong>: Store tablespace data; each database must have at least one.</li>
<li><strong>Permanent and Temporary Data Files</strong>:
<ul>
<li>Permanent tablespaces store persistent objects.</li>
<li>Temporary tablespaces use temp files for session-specific operations.</li>
</ul>
</li>
<li><strong>Online and Offline Data Files</strong>: Data files can be taken offline for maintenance.</li>
<li><strong>Data File Structure</strong>: Contains metadata (e.g., size, checkpoint SCN) and space for segments.</li>
</ul>
<h3 id="overview-of-control-files">3 Overview of Control Files</h3>
<ul>
<li><strong>Use of Control Files</strong>: Locate database files and manage the database state.</li>
<li><strong>Multiple Control Files</strong>: Multiplexing avoids single points of failure.</li>
<li><strong>Control File Structure</strong>:
<ul>
<li><strong>Circular reuse records</strong>: Noncritical, overwritable data (e.g., RMAN backups).</li>
<li><strong>Noncircular reuse records</strong>: Critical, non-overwritable data (e.g., tablespaces, data files).</li>
</ul>
</li>
</ul>
<h3 id="overview-of-the-online-redo-log">4 Overview of the Online Redo Log</h3>
<ul>
<li><strong>Use of the Online Redo Log</strong>: Protects against data loss by recording changes for recovery.</li>
<li><strong>How Oracle Database Writes to the Online Redo Log</strong>:
<ul>
<li><strong>Redo thread</strong>: Each instance has its own thread in Oracle RAC.</li>
<li><strong>Online redo log switches</strong>: Circular writing to log files.</li>
<li><strong>Multiple copies</strong>: Redundancy to prevent loss.</li>
<li><strong>Archived redo log files</strong>: Offline copies for backup/recovery.</li>
</ul>
</li>
<li><strong>Structure of the Online Redo Log</strong>: Contains redo records (change vectors) with metadata (SCN, transaction ID, operation type).</li>
</ul>
<h2 id="logical-storage-structures">13 Logical Storage Structures</h2>
<p>This chapter describes the nature of and relationships among logical storage structures, which are created and recognized by Oracle Database and are not known to the operating system.</p>
<h3 id="introduction-to-logical-storage-structures">1 Introduction to Logical Storage Structures</h3>
<ul>
<li>Oracle Database allocates logical space for all data in the database.</li>
<li><strong>Logical Storage Hierarchy</strong>:
<ul>
<li>A segment contains one or more extents, each of which contains multiple data blocks.</li>
</ul>
</li>
<li><strong>Logical Space Management</strong>:
<ul>
<li>Oracle Database uses bitmaps (for locally managed tablespaces) or the data dictionary (for dictionary-managed tablespaces) to track and allocate extents.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-data-blocks">2 Overview of Data Blocks</h3>
<ul>
<li><strong>Data Blocks and Operating System Blocks</strong>:
<ul>
<li>Oracle blocks are logical structures, while OS blocks are physical. Oracle blocks are the minimum unit of database I/O.</li>
</ul>
</li>
<li><strong>Database Block Size</strong>:
<ul>
<li>Set by <code>DB_BLOCK_SIZE</code> during database creation; default is 4 KB or 8 KB.</li>
</ul>
</li>
<li><strong>Tablespace Block Size</strong>:
<ul>
<li>Nonstandard block sizes can be specified for individual tablespaces.</li>
</ul>
</li>
<li><strong>Data Block Format</strong>:
<ul>
<li>Includes block overhead (header, table directory, row directory) and row data.</li>
</ul>
</li>
<li><strong>Row Format</strong>:
<ul>
<li>Variable-length records with row headers and column data.</li>
</ul>
</li>
<li><strong>Rowid Format</strong>:
<ul>
<li>Extended rowid includes data object number, relative file number, block number, and row number.</li>
</ul>
</li>
<li><strong>Data Block Compression</strong>:
<ul>
<li>Uses a symbol table to eliminate duplicate values in blocks.</li>
</ul>
</li>
<li><strong>Space Management in Data Blocks</strong>:
<ul>
<li><code>PCTFREE</code> reserves space for updates; free space can be optimized or coalesced.</li>
</ul>
</li>
<li><strong>Chained and Migrated Rows</strong>:
<ul>
<li>Rows too large for a single block are split (chained) or moved (migrated).</li>
</ul>
</li>
<li><strong>Overview of Index Blocks</strong>:
<ul>
<li>Index blocks (root, branch, leaf) manage space differently from table blocks.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-extents">3 Overview of Extents</h3>
<ul>
<li><strong>Allocation of Extents</strong>:
<ul>
<li>Initial extent is allocated at segment creation; incremental extents are added as needed.</li>
</ul>
</li>
<li><strong>Deallocation of Extents</strong>:
<ul>
<li>Extents are freed when objects are dropped or space is reclaimed (e.g., via segment shrink).</li>
</ul>
</li>
<li><strong>Storage Parameters for Extents</strong>:
<ul>
<li>Locally managed tablespaces use uniform or auto-allocated extents.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-segments">4 Overview of Segments</h3>
<ul>
<li><strong>User Segments</strong>:
<ul>
<li>Store data for user objects (tables, indexes, LOBs). Deferred segment creation is default.</li>
</ul>
</li>
<li><strong>Temporary Segments</strong>:
<ul>
<li>Used for sorting, hashing, and temporary tables. Stored in temp files.</li>
</ul>
</li>
<li><strong>Undo Segments</strong>:
<ul>
<li>Store undo data for transactions. Managed automatically in undo tablespaces.</li>
</ul>
</li>
<li><strong>Segment Space and the High Water Mark (HWM)</strong>:
<ul>
<li>Tracks used and unused blocks. ASSM uses bitmaps; MSSM uses free lists.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-tablespaces">5 Overview of Tablespaces</h3>
<ul>
<li><strong>Permanent Tablespaces</strong>:
<ul>
<li>Store persistent objects (e.g., <code>SYSTEM</code>, <code>SYSAUX</code>, undo tablespaces).</li>
<li><strong>SYSTEM Tablespace</strong>: Contains data dictionary and administrative objects.</li>
<li><strong>SYSAUX Tablespace</strong>: Auxiliary to <code>SYSTEM</code>, stores non-critical metadata.</li>
<li><strong>Undo Tablespaces</strong>: Store undo data for transactions.</li>
<li><strong>Shadow Tablespaces</strong>: Detect lost writes via SCN tracking.</li>
</ul>
</li>
<li><strong>Temporary Tablespaces</strong>:
<ul>
<li>Store transient data (e.g., sort operations). Can be shared or local.</li>
</ul>
</li>
<li><strong>Tablespace Modes</strong>:
<ul>
<li><strong>Read/Write vs. Read-Only</strong>: Controls write access.</li>
<li><strong>Online vs. Offline</strong>: Controls accessibility.</li>
</ul>
</li>
<li><strong>Tablespace File Size</strong>:
<ul>
<li><strong>Bigfile</strong>: Single large file (up to 128 TB). <strong>Smallfile</strong>: Multiple smaller files (default).</li>
</ul>
</li>
</ul>
<h1 id="part-v-oracle-instance-architecture">Part V: Oracle Instance Architecture</h1>
<p>This part describes the basic structural architecture of the Oracle database instance.</p>
<h2 id="oracle-database-instance">14 Oracle Database Instance</h2>
<p>This chapter explains the nature of an Oracle database instance, its associated files, and operations during startup/shutdown.</p>
<h3 id="introduction-to-the-oracle-database-instance">1 Introduction to the Oracle Database Instance</h3>
<ul>
<li><strong>Database Instance Structure</strong>:<br>
Comprises memory structures (SGA) and background processes. The SGA caches data, redo logs, and SQL plans.</li>
<li><strong>Database Instance Configurations</strong>:
<ul>
<li><strong>Single-instance</strong>: One instance per database.</li>
<li><strong>Oracle RAC</strong>: Multiple instances per database (shared storage).</li>
</ul>
</li>
<li><strong>Read/Write and Read-Only Instances</strong>:
<ul>
<li>Read/write instances handle DML.</li>
<li>Read-only instances (set via <code>INSTANCE_MODE=READ_ONLY</code>) optimize queries but disable modifications.</li>
</ul>
</li>
<li><strong>Duration of a Database Instance</strong>:<br>
Begins with <code>STARTUP</code> and ends with <code>SHUTDOWN</code>. Each instance mounts only one database.</li>
<li><strong>Identification of a Database Instance</strong>:
<ul>
<li><strong>Oracle Base Directory</strong>: Stores installation binaries (e.g., <code>/u01/app/oracle</code>).</li>
<li><strong>Oracle Home Directory</strong>: Software location (e.g., <code>/u01/app/oracle/product/12.1.0/dbhome_1</code>).</li>
<li><strong>Oracle System Identifier (SID)</strong>: Unique instance identifier (e.g., set via <code>ORACLE_SID</code>).</li>
</ul>
</li>
</ul>
<h3 id="overview-of-database-instance-startup-and-shutdown">2 Overview of Database Instance Startup and Shutdown</h3>
<ul>
<li><strong>Startup Sequence</strong>:
<ol>
<li><strong>NOMOUNT</strong>: Starts instance (reads parameter file, allocates SGA).</li>
<li><strong>MOUNT</strong>: Associates instance with database (reads control files).</li>
<li><strong>OPEN</strong>: Opens data files for user access.</li>
</ol>
</li>
<li><strong>Shutdown Sequence</strong>:
<ol>
<li><strong>CLOSE</strong>: Writes SGA data to disk.</li>
<li><strong>UNMOUNT</strong>: Disassociates database.</li>
<li><strong>SHUTDOWN</strong>: Terminates instance.</li>
</ol>
</li>
<li><strong>Shutdown Modes</strong>:
<ul>
<li><strong>ABORT</strong>: Immediate termination (requires recovery).</li>
<li><strong>IMMEDIATE</strong>: Rolls back active transactions.</li>
<li><strong>TRANSACTIONAL</strong>: Waits for transactions to complete.</li>
<li><strong>NORMAL</strong>: Waits for sessions to disconnect (default).</li>
</ul>
</li>
</ul>
<h3 id="overview-of-checkpoints">3 Overview of Checkpoints</h3>
<ul>
<li><strong>Purpose</strong>: Ensures data consistency by writing dirty buffers to disk.</li>
<li><strong>Types</strong>:
<ul>
<li><strong>Thread Checkpoints</strong>: During log switches or shutdown.</li>
<li><strong>Incremental Checkpoints</strong>: Periodic writes to reduce recovery time.</li>
</ul>
</li>
<li><strong>Checkpoint Process (CKPT)</strong>: Updates control files/data file headers with checkpoint SCN.</li>
</ul>
<h3 id="overview-of-instance-recovery">4 Overview of Instance Recovery</h3>
<ul>
<li><strong>Purpose</strong>: Recovers database after failure by reapplying redo logs (rolling forward) and undoing uncommitted changes (rolling back).</li>
<li><strong>Phases</strong>:
<ol>
<li><strong>Rolling Forward</strong>: Applies redo logs to reconstruct changes.</li>
<li><strong>Rolling Back</strong>: Undoes uncommitted transactions using undo segments.</li>
</ol>
</li>
<li><strong>Triggered by</strong>: Inconsistent shutdown (e.g., <code>SHUTDOWN ABORT</code>).</li>
</ul>
<h3 id="overview-of-parameter-files">5 Overview of Parameter Files</h3>
<ul>
<li><strong>Types</strong>:
<ul>
<li><strong>Server Parameter File (SPFILE)</strong>: Binary, persistent (recommended).</li>
<li><strong>Text Initialization File (PFILE)</strong>: Manual edits required (legacy).</li>
</ul>
</li>
<li><strong>Initialization Parameters</strong>:
<ul>
<li><strong>Basic</strong>: Essential settings (e.g., <code>DB_NAME</code>, <code>CONTROL_FILES</code>).</li>
<li><strong>Advanced</strong>: Tuning parameters (e.g., <code>SGA_TARGET</code>).</li>
</ul>
</li>
<li><strong>Modification</strong>:
<ul>
<li><strong>Static</strong>: Requires restart (e.g., <code>DB_BLOCK_SIZE</code>).</li>
<li><strong>Dynamic</strong>: Adjustable via <code>ALTER SYSTEM</code> (e.g., <code>MEMORY_TARGET</code>).</li>
</ul>
</li>
</ul>
<h3 id="overview-of-diagnostic-files">6 Overview of Diagnostic Files</h3>
<ul>
<li><strong>Automatic Diagnostic Repository (ADR)</strong>: Centralized storage for logs/traces.
<ul>
<li><strong>Structure</strong>: Organized by instance (e.g., <code>/diag/rdbms/&lt;dbname&gt;/&lt;SID&gt;</code>).</li>
</ul>
</li>
<li><strong>Alert Log</strong>: Chronological record of errors/operations (XML format).</li>
<li><strong>Trace Files</strong>:
<ul>
<li><strong>Background Processes</strong>: e.g., <code>mytest_reco_10355.trc</code>.</li>
<li><strong>Server Processes</strong>: e.g., <code>mytest_ora_10304.trc</code>.</li>
</ul>
</li>
<li><strong>Diagnostic Dumps</strong>: Detailed snapshots (e.g., heap dumps during incidents).</li>
</ul>
<h2 id="memory-architecture">15 Memory Architecture</h2>
<h3 id="introduction-to-oracle-database-memory-structures">1 Introduction to Oracle Database Memory Structures</h3>
<ul>
<li>When an instance is started, Oracle Database allocates a memory area and starts background processes.</li>
<li>Memory stores:
<ul>
<li>Program code</li>
<li>Information about each connected session</li>
<li>Information needed during program execution</li>
<li>Shared information like lock data</li>
<li>Cached data (data blocks and redo records)</li>
</ul>
</li>
</ul>
<h3 id="basic-memory-structures">2 Basic Memory Structures</h3>
<p>Oracle Database includes several memory areas, each with multiple subcomponents:</p>
<ul>
<li><strong>System Global Area (SGA)</strong>: Shared memory structures containing data and control information for one Oracle Database instance.</li>
<li><strong>Program Global Area (PGA)</strong>: Nonshared memory region for data and control information exclusive to an Oracle process.</li>
<li><strong>User Global Area (UGA)</strong>: Memory associated with a user session.</li>
<li><strong>Software Code Areas</strong>: Portions of memory storing executable code.</li>
</ul>
<h3 id="oracle-database-memory-management">3 Oracle Database Memory Management</h3>
<p>Memory management involves maintaining optimal sizes for memory structures as demands change. Options include:</p>
<ul>
<li><strong>Automatic Memory Management</strong>: Specifies target size for instance memory; automatically redistributes between SGA and PGA.</li>
<li><strong>Automatic Shared Memory Management</strong>: Partially automated; sets target size for SGA and optionally for PGA.</li>
<li><strong>Manual Memory Management</strong>: Manages SGA and PGA components individually via initialization parameters.</li>
</ul>
<h3 id="overview-of-the-user-global-area-uga">4 Overview of the User Global Area (UGA)</h3>
<ul>
<li>UGA is session memory for session variables (e.g., logon information) and session state.</li>
<li>Stores PL/SQL package state and OLAP page pool.</li>
<li>Location:
<ul>
<li><strong>Shared Server Connection</strong>: Stored in SGA.</li>
<li><strong>Dedicated Server Connection</strong>: Stored in PGA.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-the-program-global-area-pga">5 Overview of the Program Global Area (PGA)</h3>
<ul>
<li>PGA is process-specific memory, not shared with other processes.</li>
<li>Contains:
<ul>
<li><strong>Private SQL Area</strong>: Holds parsed SQL statements and session-specific processing information.</li>
<li><strong>SQL Work Areas</strong>: Used for memory-intensive operations (e.g., sorting, hash joins).</li>
</ul>
</li>
<li><strong>PGA Usage</strong>:
<ul>
<li>Dedicated Server: Private session memory.</li>
<li>Shared Server: Persistent area in SGA, runtime area in PGA.</li>
</ul>
</li>
</ul>
<h4 id="contents-of-the-pga">Contents of the PGA</h4>
<ul>
<li><strong>Private SQL Area</strong>:
<ul>
<li><strong>Runtime Area</strong>: Tracks query execution state.</li>
<li><strong>Persistent Area</strong>: Contains bind variable values.</li>
</ul>
</li>
<li><strong>SQL Work Areas</strong>: Used for sorting, hash joins, etc.</li>
</ul>
<h3 id="overview-of-the-system-global-area-sga">6 Overview of the System Global Area (SGA)</h3>
<ul>
<li>SGA is a read/write memory area shared by all server and background processes.</li>
<li>Key components:
<ul>
<li><strong>Database Buffer Cache</strong></li>
<li><strong>Redo Log Buffer</strong></li>
<li><strong>Shared Pool</strong></li>
<li><strong>Large Pool</strong></li>
<li><strong>Java Pool</strong></li>
<li><strong>Fixed SGA</strong></li>
<li><strong>Optional Performance-Related Subareas</strong> (e.g., In-Memory Area, Memoptimize Pool).</li>
</ul>
</li>
</ul>
<h4 id="database-buffer-cache">Database Buffer Cache</h4>
<ul>
<li>Stores copies of data blocks read from data files.</li>
<li><strong>Purpose</strong>:
<ul>
<li>Optimize physical I/O.</li>
<li>Keep frequently accessed blocks in memory.</li>
</ul>
</li>
<li><strong>Buffer States</strong>:
<ul>
<li>Unused, Clean, Dirty.</li>
</ul>
</li>
<li><strong>Buffer Modes</strong>:
<ul>
<li>Current Mode (db block get).</li>
<li>Consistent Mode (consistent read get).</li>
</ul>
</li>
<li><strong>Buffer I/O</strong>:
<ul>
<li>Logical I/O (reads/writes in cache).</li>
<li>Physical I/O (reads from disk).</li>
</ul>
</li>
<li><strong>Buffer Pools</strong>:
<ul>
<li>Default, Keep, Recycle pools.</li>
</ul>
</li>
<li><strong>Buffers and Full Table Scans</strong>:
<ul>
<li>Manages table scans to avoid cache thrashing.</li>
</ul>
</li>
</ul>
<h4 id="redo-log-buffer">Redo Log Buffer</h4>
<ul>
<li>Circular buffer storing redo entries for database changes.</li>
<li>Log Writer (LGWR) writes redo entries to disk sequentially.</li>
</ul>
<h4 id="shared-pool">Shared Pool</h4>
<ul>
<li>Caches program data (e.g., parsed SQL, PL/SQL code, data dictionary).</li>
<li>Subcomponents:
<ul>
<li><strong>Library Cache</strong>: Stores executable SQL and PL/SQL code.</li>
<li><strong>Data Dictionary Cache</strong>: Holds reference information about the database.</li>
<li><strong>Server Result Cache</strong>: Stores SQL query and PL/SQL function results.</li>
<li><strong>Reserved Pool</strong>: Allocates large contiguous memory chunks.</li>
</ul>
</li>
</ul>
<h4 id="large-pool">Large Pool</h4>
<ul>
<li>Optional area for large memory allocations (e.g., shared server UGAs, parallel execution buffers).</li>
<li><strong>Deferred Inserts</strong>: Buffers for MEMOPTIMIZE WRITE inserts.</li>
</ul>
<h4 id="java-pool">Java Pool</h4>
<ul>
<li>Stores session-specific Java code and data within the JVM.</li>
</ul>
<h4 id="fixed-sga">Fixed SGA</h4>
<ul>
<li>Internal housekeeping area for database state and inter-process communication.</li>
</ul>
<h4 id="optional-performance-related-sga-subareas">Optional Performance-Related SGA Subareas</h4>
<ul>
<li><strong>In-Memory Area</strong>: Stores data in columnar format for rapid scans.</li>
<li><strong>Memoptimize Pool</strong>: Optimizes key-based queries for MEMOPTIMIZE FOR READ tables.</li>
</ul>
<h3 id="overview-of-software-code-areas">Overview of Software Code Areas</h3>
<ul>
<li>Stores executable Oracle Database code.</li>
<li>Typically read-only and can be shared or nonshared.</li>
<li>Shared code reduces memory usage and improves performance.</li>
</ul>
<h2 id="process-architecture">16 Process Architecture</h2>
<h3 id="introduction-to-processes">1 Introduction to Processes</h3>
<ul>
<li>A process is a mechanism in an operating system that can run a series of steps.</li>
<li><strong>Execution Architecture</strong>:
<ul>
<li>On Windows: Oracle background processes are threads within a process.</li>
<li>On Linux/UNIX: Oracle processes are either OS processes or threads within an OS process.</li>
</ul>
</li>
<li><strong>Processes run code modules</strong>:
<ul>
<li><strong>Application or Oracle Database utility</strong>: Issues SQL statements.</li>
<li><strong>Oracle database code</strong>: Interprets and processes SQL statements.</li>
</ul>
</li>
<li>Processes write to trace files periodically.</li>
</ul>
<h4 id="types-of-processes">Types of Processes</h4>
<ul>
<li><strong>Client Process</strong>: Runs application or Oracle tool code.</li>
<li><strong>Oracle Process</strong>: Runs Oracle database code, including:
<ul>
<li><strong>Background Process</strong>: Performs maintenance tasks (e.g., instance recovery, writing redo buffers to disk).</li>
<li><strong>Server Process</strong>: Handles client requests (e.g., parsing SQL queries, reading buffers).</li>
</ul>
</li>
<li><strong>Slave Process</strong>: Performs additional tasks for background or server processes.</li>
</ul>
<h4 id="multiprocess-and-multithreaded-oracle-database-systems">Multiprocess and Multithreaded Oracle Database Systems</h4>
<ul>
<li><strong>Multiprocess Oracle Database</strong>: Uses multiple processes to run different parts of Oracle Database code.</li>
<li><strong>Multithreaded Model (Oracle Database 12c and later)</strong>:
<ul>
<li>Oracle processes can execute as OS threads in separate address spaces.</li>
<li>Enabled by setting <code>THREADED_EXECUTION</code> initialization parameter to <code>TRUE</code>.</li>
<li>Example: PMON and DBW run as OS processes, while LGWR and CMON run as threads within a single process.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-client-processes">2 Overview of Client Processes</h3>
<ul>
<li>Created when a user runs an application (e.g., SQL<em>Plus, Pro</em>C program).</li>
<li><strong>Key Features</strong>:
<ul>
<li>Cannot read/write to SGA directly.</li>
<li>Can run on a host different from the database host.</li>
</ul>
</li>
</ul>
<h4 id="client-and-server-processes">Client and Server Processes</h4>
<ul>
<li><strong>Differences</strong>:
<ul>
<li>Server processes interact directly with the instance; client processes do not.</li>
<li>Server processes can run on the database host only.</li>
</ul>
</li>
</ul>
<h4 id="connections-and-sessions">Connections and Sessions</h4>
<ul>
<li><strong>Connection</strong>: Physical communication pathway between a client process and a database instance.</li>
<li><strong>Session</strong>: Logical entity representing a user login state.
<ul>
<li>A single connection can have multiple sessions.</li>
<li>Sessions are independent (e.g., commits in one session do not affect others).</li>
</ul>
</li>
<li><strong>Examples</strong>:
<ul>
<li>Dedicated server: One server process per connection.</li>
<li>Shared server: Multiple client processes share a single server process.</li>
</ul>
</li>
</ul>
<h4 id="database-operations">Database Operations</h4>
<ul>
<li>Defined as session activity between two points in time.</li>
<li><strong>Types</strong>:
<ul>
<li><strong>Simple</strong>: Single SQL statement or PL/SQL procedure.</li>
<li><strong>Composite</strong>: Set of single or composite operations.</li>
</ul>
</li>
<li><strong>Monitoring</strong>: Managed via <code>DBMS_SQL_MONITOR</code> PL/SQL package and views like <code>V$SQL_MONITOR</code>.</li>
</ul>
<h3 id="overview-of-server-processes">3 Overview of Server Processes</h3>
<ul>
<li>Created to handle client process requests.</li>
<li><strong>Tasks</strong>:
<ul>
<li>Parse and execute SQL statements.</li>
<li>Read data blocks into the buffer cache.</li>
<li>Return results to the client.</li>
</ul>
</li>
</ul>
<h4 id="dedicated-server-processes">Dedicated Server Processes</h4>
<ul>
<li>One server process per client connection.</li>
<li><strong>Features</strong>:
<ul>
<li>Stores process-specific info and UGA in PGA.</li>
<li>Direct communication between client and server.</li>
</ul>
</li>
</ul>
<h4 id="shared-server-processes">Shared Server Processes</h4>
<ul>
<li>Multiple client processes connect to a dispatcher process.</li>
<li><strong>Workflow</strong>:
<ol>
<li>Dispatcher places requests in a request queue (in the large pool).</li>
<li>Shared server processes pick requests from the queue.</li>
<li>Results are placed in the dispatcher’s response queue.</li>
</ol>
</li>
<li><strong>UGA</strong>: Stored in SGA for shared access.</li>
</ul>
<h4 id="how-oracle-database-creates-server-processes">How Oracle Database Creates Server Processes</h4>
<ul>
<li><strong>Connection Methods</strong>:
<ul>
<li><strong>Bequeath</strong>: Client directly spawns the server process.</li>
<li><strong>Oracle Net Listener</strong>: Client connects via a listener.</li>
<li><strong>Dedicated Broker</strong>: Listener hands off connection to a broker within the instance.</li>
</ul>
</li>
<li><strong>Optimization</strong>: Pre-created server processes (via <code>DBMS_PROCESS</code>) improve performance.</li>
</ul>
<h3 id="overview-of-background-processes">4 Overview of Background Processes</h3>
<ul>
<li>Perform maintenance tasks for database operation and performance.</li>
<li><strong>Types</strong>:
<ul>
<li><strong>Mandatory</strong>: Present in all typical configurations.</li>
<li><strong>Optional</strong>: Specific to tasks or features.</li>
</ul>
</li>
</ul>
<h4 id="mandatory-background-processes">Mandatory Background Processes</h4>
<ul>
<li><strong>Process Monitor Process (PMON) Group</strong>:
<ul>
<li>Includes PMON, CLMN, and CLnn.</li>
<li>Cleans up terminated processes and releases resources.</li>
</ul>
</li>
<li><strong>Process Manager (PMAN)</strong>:
<ul>
<li>Oversees shared servers, pooled servers, and job queue processes.</li>
</ul>
</li>
<li><strong>Listener Registration Process (LREG)</strong>:
<ul>
<li>Registers instance and dispatcher info with the Oracle Net Listener.</li>
</ul>
</li>
<li><strong>System Monitor Process (SMON)</strong>:
<ul>
<li>Performs instance recovery, cleans up temporary segments, and coalesces free extents.</li>
</ul>
</li>
<li><strong>Database Writer Process (DBW)</strong>:
<ul>
<li>Writes dirty buffers from the buffer cache to disk.</li>
</ul>
</li>
<li><strong>Log Writer Process (LGWR)</strong>:
<ul>
<li>Manages the redo log buffer and writes redo entries to disk.</li>
</ul>
</li>
<li><strong>Checkpoint Process (CKPT)</strong>:
<ul>
<li>Updates control files and data file headers with checkpoint info.</li>
</ul>
</li>
<li><strong>Manageability Monitor Processes (MMON and MMNL)</strong>:
<ul>
<li>MMON handles AWR tasks; MMNL writes ASH buffer data to disk.</li>
</ul>
</li>
<li><strong>Recoverer Process (RECO)</strong>:
<ul>
<li>Resolves failures in distributed transactions.</li>
</ul>
</li>
</ul>
<h4 id="optional-background-processes">Optional Background Processes</h4>
<ul>
<li><strong>Archiver Processes (ARCn)</strong>:
<ul>
<li>Copy online redo logs to offline storage (in ARCHIVELOG mode).</li>
</ul>
</li>
<li><strong>Job Queue Processes (CJQ0 and Jnnn)</strong>:
<ul>
<li>Run user jobs in batch mode.</li>
</ul>
</li>
<li><strong>Flashback Data Archive Process (FBDA)</strong>:
<ul>
<li>Archives historical rows for tracked tables.</li>
</ul>
</li>
<li><strong>Space Management Coordinator Process (SMCO)</strong>:
<ul>
<li>Coordinates space-related tasks (e.g., proactive allocation, reclamation).</li>
</ul>
</li>
</ul>
<h4 id="slave-processes">Slave Processes</h4>
<ul>
<li>Perform work on behalf of other processes.</li>
<li><strong>Types</strong>:
<ul>
<li><strong>I/O Slave Processes (Innn)</strong>:
<ul>
<li>Simulate asynchronous I/O for systems that lack support.</li>
</ul>
</li>
<li><strong>Parallel Execution (PX) Server Processes</strong>:
<ul>
<li>Work together to execute a single SQL statement in parallel.</li>
<li><strong>Query Coordinator</strong>: Parses the query, allocates PX servers, and integrates results.</li>
<li><strong>Producers and Consumers</strong>: Producers process data; consumers receive and use it.</li>
<li><strong>Granules</strong>: Smallest units of work (e.g., blocks of a table scanned by a PX server).<br>
``</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2 id="application-and-oracle-net-services-architecture">17 Application and Oracle Net Services Architecture</h2>
<h3 id="overview-of-oracle-application-architecture">1 Overview of Oracle Application Architecture</h3>
<ul>
<li><strong>Definition</strong>: Computing environment where a database application connects to an Oracle database.</li>
<li><strong>Key Architectures</strong>:
<ul>
<li><strong>Client/Server Architecture</strong></li>
<li><strong>Multitier Architecture</strong></li>
<li><strong>Grid Architecture</strong></li>
</ul>
</li>
</ul>
<h4 id="overview-of-clientserver-architecture">Overview of Client/Server Architecture</h4>
<ul>
<li><strong>Components</strong>:
<ul>
<li><strong>Client</strong>: Runs the database application (e.g., SQL*Plus, Visual Basic).</li>
<li><strong>Server</strong>: Runs Oracle Database software, handles shared data access.</li>
</ul>
</li>
<li><strong>Distributed Processing</strong>:
<ul>
<li>Front-end (client) and back-end (server) processing occur on different computers.</li>
<li>Example: Client on one host accesses a database on another host via Oracle Net Services.</li>
</ul>
</li>
<li><strong>Advantages</strong>:
<ul>
<li>Clients focus on input/output; servers handle data processing.</li>
<li>Data location transparency.</li>
<li>Scalability (horizontal and vertical).</li>
<li>Efficient resource use (e.g., client workstations optimized for display, servers for storage).</li>
</ul>
</li>
</ul>
<h4 id="overview-of-multitier-architecture">Overview of Multitier Architecture</h4>
<ul>
<li><strong>Components</strong>:
<ul>
<li><strong>Clients</strong>: Initiate requests (e.g., Web browsers).</li>
<li><strong>Application Servers</strong>: Interface between clients and database servers; validate credentials, perform operations.</li>
<li><strong>Database Servers</strong>: Execute queries and provide data.</li>
</ul>
</li>
<li><strong>Service-Oriented Architecture (SOA)</strong>:
<ul>
<li>Database serves as a Web service provider.</li>
<li>Supports XML standards (WSDL, SOAP).</li>
<li>Enables SQL/XQuery queries and PL/SQL function calls via HTTP.</li>
</ul>
</li>
</ul>
<h4 id="overview-of-grid-architecture">Overview of Grid Architecture</h4>
<ul>
<li><strong>Definition</strong>: Pools servers and storage into flexible, on-demand resources.</li>
<li><strong>Benefits</strong>: Modularity, scalability, and efficient resource utilization.</li>
</ul>
<h3 id="overview-of-oracle-net-services-architecture">2 Overview of Oracle Net Services Architecture</h3>
<ul>
<li><strong>Purpose</strong>: Provides enterprise-wide connectivity in distributed environments.</li>
<li><strong>Features</strong>:
<ul>
<li>Location transparency.</li>
<li>Centralized configuration.</li>
<li>Supports shared server architecture for scalability.</li>
</ul>
</li>
</ul>
<h4 id="how-oracle-net-services-works">How Oracle Net Services Works</h4>
<ul>
<li>Packages SQL statements for transmission via supported protocols.</li>
<li>Operates independently of the network OS.</li>
</ul>
<h4 id="the-oracle-net-listener">The Oracle Net Listener</h4>
<ul>
<li><strong>Role</strong>: Listens for client connection requests and routes traffic.</li>
<li><strong>Service Registration</strong>:
<ul>
<li>LREG process dynamically registers instance info (service names, handlers) with the listener.</li>
<li>Enables load balancing and failover.</li>
</ul>
</li>
<li><strong>Service Names</strong>: Logical identifiers for client connections (e.g., <code>book.example.com</code>).</li>
</ul>
<h4 id="dedicated-server-architecture">Dedicated Server Architecture</h4>
<ul>
<li><strong>Description</strong>: One server process per client connection.</li>
<li><strong>Workflow</strong>:
<ul>
<li>Client connects to a dedicated server process.</li>
<li>Process remains active even when idle.</li>
</ul>
</li>
<li><strong>Use Case</strong>: Best for long-lived connections with high activity.</li>
</ul>
<h4 id="shared-server-architecture">Shared Server Architecture</h4>
<ul>
<li><strong>Description</strong>: Dispatchers route client requests to a pool of shared server processes.</li>
<li><strong>Components</strong>:
<ul>
<li><strong>Dispatcher Processes (Dnnn)</strong>: Manage client connections.</li>
<li><strong>Shared Server Processes (Snnn)</strong>: Handle requests from a common queue.</li>
</ul>
</li>
<li><strong>Advantages</strong>:
<ul>
<li>Reduces OS processes and PGA memory.</li>
<li>Scales to more simultaneous connections.</li>
</ul>
</li>
<li><strong>Disadvantages</strong>: Slower response for some operations; complex setup.</li>
<li><strong>Restrictions</strong>: Certain admin tasks (e.g., shutdown) require dedicated connections.</li>
</ul>
<h4 id="database-resident-connection-pooling-drcp">Database Resident Connection Pooling (DRCP)</h4>
<ul>
<li><strong>Purpose</strong>: Provides a pool of dedicated servers for short-lived connections (e.g., Web apps).</li>
<li><strong>Workflow</strong>:
<ul>
<li>Connection broker assigns pooled servers to clients.</li>
<li>Servers return to the pool after use.</li>
</ul>
</li>
<li><strong>Benefits</strong>:
<ul>
<li>Reduces memory usage.</li>
<li>Scales to tens of thousands of connections.</li>
<li>Compatible with multi-process apps (e.g., PHP, Apache).</li>
</ul>
</li>
</ul>
<h3 id="overview-of-the-program-interface">3 Overview of the Program Interface</h3>
<ul>
<li><strong>Role</strong>: Acts as a security and communication layer between apps and the database.</li>
<li><strong>Functions</strong>:
<ul>
<li>Converts data types.</li>
<li>Traps errors.</li>
<li>Formats requests.</li>
</ul>
</li>
</ul>
<h4 id="program-interface-structure">Program Interface Structure</h4>
<ul>
<li><strong>Components</strong>:
<ul>
<li><strong>Oracle Call Interface (OCI)</strong>: Client-side library.</li>
<li><strong>Oracle Net Services Drivers</strong>: Protocol-specific (e.g., TCP/IP).</li>
<li><strong>Operating System Communications Software</strong>: Lowest-level link (e.g., DECnet, TCP/IP).</li>
</ul>
</li>
</ul>
<h4 id="program-interface-drivers">Program Interface Drivers</h4>
<ul>
<li><strong>Role</strong>: Transport data across networks.</li>
<li><strong>Examples</strong>: Asynchronous, DECnet drivers.</li>
<li><strong>Flexibility</strong>: Multiple drivers can coexist; apps can switch dynamically.</li>
</ul>
<h4 id="communications-software-for-the-operating-system">Communications Software for the Operating System</h4>
<ul>
<li><strong>Examples</strong>: TCP/IP, LU6.2.</li>
<li><strong>Integration</strong>: Provided by OS vendors or third parties; interfaces with Oracle Net Services.</li>
</ul>
<h1 id="part-vi-oracle-database-administration-and-application-development">Part VI: Oracle Database Administration and Application Development</h1>
<p>This part covers essential topics for database administrators and application developers.</p>
<h2 id="topics-for-database-administrators-and-developers">18 Topics for Database Administrators and Developers</h2>
<h3 id="overview-of-database-security">1 Overview of Database Security</h3>
<ul>
<li><strong>Database Security</strong>: Involves user authentication, encryption, access control, and monitoring.
<ul>
<li><strong>User Accounts</strong>: Lists valid database users, including default accounts like <code>SYSTEM</code>.</li>
<li><strong>Database Authentication</strong>: Methods include passwords, Kerberos tickets, and PKI certificates.</li>
<li><strong>Encryption</strong>: Transforms data into an unreadable format (e.g., Transparent Data Encryption).</li>
<li><strong>Oracle Data Redaction</strong>: Masks data for low-privileged users in real-time.</li>
<li><strong>Orientation</strong>: Techniques like Oracle Database Vault, Virtual Private Database (VPD), and Oracle Label Security (OLS).</li>
<li><strong>Data Access Monitoring</strong>: Tools include auditing and Oracle Audit Vault.</li>
</ul>
</li>
</ul>
<h4 id="privileges">Privileges</h4>
<ul>
<li><strong>System Privilege</strong>: Right to perform actions (e.g., <code>CREATE_USER</code>).</li>
<li><strong>Object Privilege</strong>: Right to perform actions on specific objects (e.g., querying a table).</li>
</ul>
<h4 id="roles">Roles</h4>
<ul>
<li>Named groups of related privileges assigned to users or roles (e.g., <code>PAY_CLERK</code>, <code>MANAGER</code>).</li>
</ul>
<h4 id="privilege-analysis">Privilege Analysis</h4>
<ul>
<li>Captures privilege usage to identify unnecessary grants and improve security.</li>
</ul>
<h4 id="user-profiles">User Profiles</h4>
<ul>
<li>Named sets of resource limits and password parameters to restrict database usage.</li>
</ul>
<h3 id="overview-of-high-availability">2 Overview of High Availability</h3>
<ul>
<li><strong>Availability</strong>: Degree to which an application/service is accessible.
<ul>
<li><strong>Unplanned Downtime</strong>: Solutions for site, computer, storage failures, data corruption, and human errors.</li>
<li><strong>Planned Downtime</strong>: Minimizing disruptions during maintenance or upgrades.</li>
</ul>
</li>
</ul>
<h4 id="high-availability-solutions">High Availability Solutions</h4>
<ul>
<li><strong>Oracle Data Guard</strong>: Maintains standby databases for failover.</li>
<li><strong>Fast Start Fault Recovery</strong>: Bounds instance recovery time.</li>
<li><strong>Oracle Flashback Technology</strong>: Corrects human errors (e.g., row/table recovery).</li>
</ul>
<h3 id="overview-of-grid-computing">3 Overview of Grid Computing</h3>
<ul>
<li><strong>Grid Computing</strong>: Pools servers and storage for flexible resource allocation.
<ul>
<li><strong>Database Server Grid</strong>: Uses Oracle RAC for scalable, fault-tolerant clusters.</li>
<li><strong>Oracle Flex Clusters</strong>: Supports large hub-and-spoke node configurations.</li>
<li><strong>Database Storage Grid</strong>: Managed via Oracle ASM for efficient data distribution.</li>
</ul>
</li>
</ul>
<h3 id="overview-of-data-warehousing-and-business-intelligence">4 Overview of Data Warehousing and Business Intelligence</h3>
<ul>
<li><strong>Data Warehouse</strong>: Relational database for query/analysis (not transaction processing).
<ul>
<li><strong>ETL Process</strong>: Extraction, Transformation, Loading of data.</li>
<li><strong>Business Intelligence</strong>: Analytic SQL, OLAP, and Oracle Advanced Analytics (e.g., data mining).</li>
</ul>
</li>
</ul>
<h4 id="data-warehouse-architectures">Data Warehouse Architectures</h4>
<ol>
<li><strong>Basic</strong>: Direct user access to warehouse data.</li>
<li><strong>Staging Area</strong>: Preprocesses data before loading.</li>
<li><strong>Data Marts</strong>: Customized warehouses for specific business units.</li>
</ol>
<h3 id="overview-of-oracle-information-integration">5 Overview of Oracle Information Integration</h3>
<ul>
<li><strong>Consolidation</strong>: Centralizing data into a single database.</li>
<li><strong>Federation</strong>: Virtual integration of distributed data.</li>
<li><strong>Sharing</strong>: Asynchronous data replication (e.g., Oracle GoldenGate, Advanced Queuing).</li>
</ul>
<h4 id="federated-access">Federated Access</h4>
<ul>
<li><strong>Distributed SQL</strong>: Queries/updates across multiple databases.</li>
<li><strong>Database Links</strong>: Connections enabling access to remote databases.</li>
</ul>
<h4 id="information-sharing">Information Sharing</h4>
<ul>
<li><strong>Oracle GoldenGate</strong>: Real-time, heterogeneous data replication.</li>
<li><strong>Advanced Queuing (AQ)</strong>: Message queuing for application integration.</li>
</ul>
<h2 id="concepts-for-database-administrators">19 Concepts for Database Administrators</h2>
<p>This chapter describes the duties, tools, and essential knowledge for database administrators (DBAs).</p>
<h3 id="duties-of-database-administrators">1 Duties of Database Administrators</h3>
<p>The principal responsibility of a DBA is to ensure enterprise data is available to users. DBAs collaborate with developers and system administrators to optimize database performance and resource usage.</p>
<h4 id="key-tasks">Key Tasks:</h4>
<ul>
<li>Install, upgrade, and patch Oracle Database software.</li>
<li>Design databases (logical and physical).</li>
<li>Create and manage Oracle databases.</li>
<li>Develop and test backup/recovery strategies.</li>
<li>Configure network environments for client connections.</li>
<li>Start up/shut down databases.</li>
<li>Manage storage, users, security, and database objects (tables, indexes, views).</li>
<li>Monitor and tune database performance.</li>
<li>Report critical errors to Oracle Support.</li>
<li>Evaluate new database features.</li>
</ul>
<h4 id="roles-1">Roles:</h4>
<ul>
<li>Small databases: Single DBA.</li>
<li>Large databases: Specialized roles (e.g., security officers, backup operators).</li>
</ul>
<h3 id="tools-for-database-administrators">2 Tools for Database Administrators</h3>
<p>Oracle provides several tools for database administration:</p>
<h4 id="oracle-enterprise-manager">Oracle Enterprise Manager</h4>
<ul>
<li><strong>Oracle Enterprise Manager Cloud Control</strong>: Web-based interface for monitoring Oracle and non-Oracle components.
<ul>
<li>Components:
<ul>
<li>Oracle Management Service (OMS).</li>
<li>Oracle Management Agents.</li>
<li>Oracle Management Repository.</li>
</ul>
</li>
</ul>
</li>
<li><strong>Oracle Enterprise Manager Database Express (EM Express)</strong>: Built-in web management tool for basic administration and performance monitoring.</li>
</ul>
<h4 id="sqlplus">SQL*Plus</h4>
<ul>
<li>Interactive/batch query tool for executing SQL, PL/SQL, and OS commands.</li>
<li>Features: Formatting query results, generating reports, administering databases.</li>
</ul>
<h4 id="tools-for-database-installation-and-configuration">Tools for Database Installation and Configuration</h4>
<ul>
<li><strong>Oracle Universal Installer (OUI)</strong>: GUI for installing/uninstalling Oracle software.</li>
<li><strong>Database Upgrade Assistant (DBUA)</strong>: Guides database upgrades.</li>
<li><strong>Database Configuration Assistant (DBCA)</strong>: Creates/configures databases using templates.</li>
</ul>
<h4 id="tools-for-oracle-net-configuration-and-administration">Tools for Oracle Net Configuration and Administration</h4>
<ul>
<li><strong>Oracle Net Manager</strong>: Configures naming methods, profiles, and listeners.</li>
<li><strong>Oracle Net Configuration Assistant</strong>: Configures basic network components during installation.</li>
<li><strong>Listener Control Utility</strong>: Manages client connection listeners.</li>
<li><strong>Oracle Connection Manager Control Utility</strong>: Administers Oracle Connection Manager.</li>
</ul>
<h4 id="tools-for-data-movement-and-analysis">Tools for Data Movement and Analysis</h4>
<ul>
<li><strong>SQL*Loader</strong>: Loads data from external files into tables.</li>
<li><strong>Oracle Data Pump Export/Import</strong>: Moves data/metadata between databases.</li>
<li><strong>Oracle LogMiner</strong>: Queries redo log files via SQL.</li>
<li><strong>ADR Command Interpreter (ADRCI)</strong>: Investigates problems and manages diagnostic data.</li>
</ul>
<h3 id="topics-for-database-administrators">3 Topics for Database Administrators</h3>
<h4 id="backup-and-recovery">Backup and Recovery</h4>
<ul>
<li><strong>Backup and Recovery Techniques</strong>:
<ul>
<li><strong>Recovery Manager (RMAN)</strong>: Integrated tool for backups, restores, and recovery.</li>
<li><strong>User-Managed Techniques</strong>: Manual backups using OS commands.</li>
</ul>
</li>
<li><strong>Recovery Manager Architecture</strong>: RMAN integrates with Oracle Secure Backup and Cloud Control.</li>
<li><strong>Database Backups</strong>:
<ul>
<li><strong>Physical Backups</strong>: Copies of database files (data files, control files).</li>
<li><strong>Logical Backups</strong>: Exported data (e.g., using Data Pump).</li>
<li><strong>Whole/Partial Backups</strong>: Back up entire databases or subsets (tablespaces/data files).</li>
<li><strong>Consistent/Inconsistent Backups</strong>: Consistent backups require shutdown; inconsistent backups allow online operations.</li>
<li><strong>Backup Sets/Image Copies</strong>: RMAN can create proprietary backup sets or bit-for-bit image copies.</li>
</ul>
</li>
<li><strong>Data Repair</strong>:
<ul>
<li><strong>Oracle Flashback Technology</strong>: Rewinds data to previous states without backups.</li>
<li><strong>Data Recovery Advisor</strong>: Diagnoses failures and suggests repairs.</li>
<li><strong>Block Media Recovery</strong>: Fixes corrupt data blocks while files are online.</li>
<li><strong>Data File Recovery</strong>: Restores lost/damaged files (complete/incomplete recovery).</li>
</ul>
</li>
<li><strong>Zero Data Loss Recovery Appliance</strong>: Centralized backup solution for enterprise databases.</li>
</ul>
<p><strong>See Also:</strong></p>
<ul>
<li><em>Oracle Database Backup and Recovery User’s Guide</em>.</li>
</ul>
<h4 id="memory-management">Memory Management</h4>
<ul>
<li><strong>Automatic Memory Management</strong>: Oracle manages SGA and PGA memory automatically (<code>MEMORY_TARGET</code>).</li>
<li><strong>Shared Memory Management</strong>:
<ul>
<li><strong>Automatic Shared Memory Management</strong>: Oracle tunes SGA components (<code>SGA_TARGET</code>).</li>
<li><strong>Manual Shared Memory Management</strong>: DBA manually configures SGA components.</li>
</ul>
</li>
<li><strong>Instance PGA Management</strong>:
<ul>
<li><strong>Automatic PGA Management</strong>: Oracle tunes PGA memory (<code>PGA_AGGREGATE_TARGET</code>).</li>
<li><strong>Manual PGA Management</strong>: DBA sets work area sizes manually.</li>
</ul>
</li>
</ul>
<h4 id="resource-management-and-task-scheduling">Resource Management and Task Scheduling</h4>
<ul>
<li><strong>Database Resource Manager</strong>: Allocates resources (CPU, memory) to user groups.
<ul>
<li>Features: Controls runaway queries, prioritizes workloads.</li>
</ul>
</li>
<li><strong>Oracle Scheduler</strong>: Schedules jobs based on time/events.
<ul>
<li>Components: Programs, schedules, jobs.</li>
</ul>
</li>
</ul>
<h4 id="performance-and-tuning">Performance and Tuning</h4>
<ul>
<li><strong>Database Self-Monitoring</strong>: Alerts for performance issues.</li>
<li><strong>Automatic Workload Repository (AWR)</strong>: Repository of performance statistics.</li>
<li><strong>Automatic Database Monitor (ADDM)</strong>: Diagnoses performance issues using AWR data.</li>
<li><strong>Active Session History (ASH)</strong>: Samples active sessions for troubleshooting.</li>
<li><strong>Application and SQL Tuning</strong>:
<ul>
<li><strong>EXPLAIN PLAN</strong>: Views optimizer execution plans.</li>
<li><strong>Optimizer Statistics Advisor</strong>: Analyzes statistics quality.</li>
<li><strong>SQL Tuning Advisor</strong>: Recommends SQL improvements.</li>
<li><strong>SQL Access Advisor</strong>: Optimizes schema objects (indexes, materialized views).</li>
<li><strong>SQL Plan Management</strong>: Manages execution plans for stability.</li>
</ul>
</li>
</ul>
<h2 id="concepts-for-database-developers">20 Concepts for Database Developers</h2>
<p>This chapter provides an overview of the duties, tools, and essential topics for Oracle Database developers.</p>
<h3 id="duties-of-database-developers">1 Duties of Database Developers</h3>
<p>Oracle developers are responsible for creating/maintaining database components of applications using Oracle technology stack.</p>
<h4 id="key-tasks-1">Key Tasks:</h4>
<ul>
<li>Implement data models required by applications.</li>
<li>Create schema objects (tables, views, indexes).</li>
<li>Implement data integrity rules (constraints).</li>
<li>Choose programming environments (e.g., PL/SQL, Java).</li>
<li>Write server-side PL/SQL/Java and client-side code with SQL.</li>
<li>Develop application interfaces using chosen tools.</li>
<li>Establish Globalization Support for multilingual apps.</li>
<li>Deploy applications across different environments (dev, test, production).</li>
</ul>
<h3 id="tools-for-database-developers">2 Tools for Database Developers</h3>
<p>Oracle provides several integrated development tools:</p>
<h4 id="sql-developer">1- SQL Developer</h4>
<ul>
<li>Graphical version of SQL*Plus with Java-based interface.</li>
<li>Features:
<ul>
<li>Browse/create/edit schema objects.</li>
<li>Execute SQL statements.</li>
<li>Debug PL/SQL.</li>
<li>Export data and generate reports.</li>
</ul>
</li>
<li>Included in default Oracle installations.</li>
</ul>
<h4 id="oracle-application-express-apex">2- Oracle Application Express (APEX)</h4>
<ul>
<li>Web-based rapid application development tool.</li>
<li>Uses PL/SQL for backend logic and HTML for frontend rendering.</li>
<li>Simplifies architecture by eliminating middle-tier (embedded PL/SQL gateway).</li>
</ul>
<h4 id="oracle-jdeveloper">3- Oracle JDeveloper</h4>
<ul>
<li>Integrated Development Environment (IDE) for Java, XML, and Web services.</li>
<li>Supports full software development lifecycle (modeling, coding, debugging, deployment).</li>
</ul>
<h4 id="oracle-developer-tools-for-visual-studio-.net">4- Oracle Developer Tools for Visual Studio .NET</h4>
<ul>
<li>Integrates Oracle functionality into Visual Studio .NET.</li>
<li>Supports .NET stored procedures in VB/C# with SQL/PL/SQL.</li>
</ul>
<h3 id="topics-for-database-developers">3 Topics for Database Developers</h3>
<h4 id="principles-of-application-design-and-tuning">1- Principles of Application Design and Tuning</h4>
<p><strong>Best Practices:</strong></p>
<ul>
<li>Use bind variables to enable soft parsing and reuse query plans.</li>
<li>Implement integrity constraints in the database (not client code).</li>
<li>Build test environments with representative data.</li>
<li>Design data models for performance (avoid generic models).</li>
<li>Instrument code for debugging and performance monitoring.</li>
</ul>
<h4 id="client-side-database-programming">2- Client-Side Database Programming</h4>
<p>Two primary techniques:</p>
<h4 id="embedded-sql">Embedded SQL</h4>
<ul>
<li><strong>Oracle Precompilers</strong> (Pro<em>C/C++, Pro</em>COBOL):
<ul>
<li>Embed SQL in high-level languages (C, C++, COBOL).</li>
<li>Translates SQL to runtime library calls.</li>
</ul>
</li>
<li><strong>SQLJ</strong>:
<ul>
<li>ANSI standard for embedding SQL in Java.</li>
<li>Simpler alternative to JDBC.</li>
</ul>
</li>
</ul>
<h4 id="client-side-apis">Client-Side APIs</h4>
<ul>
<li><strong>OCI/OCCI</strong>:
<ul>
<li>Oracle Call Interface © and Oracle C++ Call Interface.</li>
<li>High-performance, low-level control.</li>
</ul>
</li>
<li><strong>ODBC/JDBC</strong>:
<ul>
<li>Standard APIs for database connectivity (ODBC for VB/.NET, JDBC for Java).</li>
<li>Oracle provides JDBC drivers (Thin for pure Java, OCI for client-side).</li>
</ul>
</li>
</ul>
<h4 id="globalization-support">3- Globalization Support</h4>
<p><strong>Key Features:</strong></p>
<ul>
<li>Store/process data in native languages (Unicode support).</li>
<li>Local formats for dates, numbers, currencies.</li>
<li>Calendar systems (Gregorian, Japanese Imperial).</li>
</ul>
<h4 id="globalization-support-environment">Globalization Support Environment</h4>
<ul>
<li><strong>Character Sets</strong>:
<ul>
<li>Database vs. client character sets (e.g., UTF-8, AL32UTF8).</li>
</ul>
</li>
<li><strong>Locale-Specific Settings</strong>:
<ul>
<li>NLS parameters control language/territory behavior (e.g., <code>NLS_LANG</code>).</li>
</ul>
</li>
</ul>
<h4 id="oracle-globalization-development-kit-gdk">Oracle Globalization Development Kit (GDK)</h4>
<ul>
<li>APIs for Java/PL/SQL to simplify global app development.</li>
</ul>
<h4 id="unstructured-data">4- Unstructured Data</h4>
<p>Support for non-relational data types:</p>
<h4 id="overview-of-xml-in-oracle-database">Overview of XML in Oracle Database</h4>
<ul>
<li><strong>Oracle XML DB</strong>:
<ul>
<li>Native <code>XMLType</code> storage.</li>
<li>Supports XML Schema, XQuery, XPath.</li>
<li>Example:<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">CREATE</span> <span class="token keyword">TABLE</span> orders <span class="token keyword">OF</span> XMLType<span class="token punctuation">;</span>
<span class="token keyword">INSERT</span> <span class="token keyword">INTO</span> orders <span class="token keyword">VALUES</span> <span class="token punctuation">(</span>XMLType<span class="token punctuation">(</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
</li>
</ul>
</li>
</ul>
<h4 id="overview-of-json-in-oracle-database">Overview of JSON in Oracle Database</h4>
<ul>
<li>Native JSON support with SQL/PL/SQL APIs.</li>
<li>Store JSON in <code>VARCHAR2</code>, <code>CLOB</code>, or <code>BLOB</code>.</li>
<li>Query with <code>JSON_TABLE</code>, <code>JSON_QUERY</code>.</li>
<li>Example:<pre class=" language-sql"><code class="prism  language-sql"><span class="token keyword">CREATE</span> <span class="token keyword">TABLE</span> j_purchaseorder <span class="token punctuation">(</span>
    po_document CLOB <span class="token keyword">CHECK</span> <span class="token punctuation">(</span>po_document <span class="token operator">IS</span> JSON<span class="token punctuation">)</span>
<span class="token punctuation">)</span><span class="token punctuation">;</span>

</code></pre>
</li>
</ul>
<h4 id="overview-of-lobs">Overview of LOBs</h4>
<ul>
<li>
<p><strong>Internal LOBs</strong>:</p>
<ul>
<li><code>CLOB</code>  (text),  <code>NCLOB</code>  (Unicode),  <code>BLOB</code>  (binary).</li>
</ul>
</li>
<li>
<p><strong>External LOBs</strong>:</p>
<ul>
<li><code>BFILE</code>  (read-only external files).</li>
</ul>
</li>
<li>
<p><strong>SecureFiles</strong>:</p>
<ul>
<li>Advanced features (compression, encryption).</li>
</ul>
</li>
</ul>
<h4 id="overview-of-oracle-text">Overview of Oracle Text</h4>
<ul>
<li>
<p>Full-text search for documents/web content.</p>
</li>
<li>
<p>Supports mixed queries (text + structured data).</p>
</li>
</ul>
<h4 id="overview-of-oracle-spatial-and-graph">Overview of Oracle Spatial and Graph</h4>
<ul>
<li>
<p>Spatial data (e.g., maps with longitude/latitude).</p>
</li>
<li>
<p>Graph data (social networks, semantic graphs).</p>
</li>
</ul>

