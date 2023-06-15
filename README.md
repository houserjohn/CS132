# CS132
## 4/4/2023 Week 1 Tuesday Lec 1
* Abstract view vs. Two pass compiler
* scanner remove non-useful characters and produce tokens
* Scanner
    * Specifying patterns
    * Can change char.class and next.state to change languages
## 4/6/2023 Week 1 Thursday Lec 2
* Chapter 3: LL Parsing
* Notatiion
    * lowercase token
    * uppercase nonterminal
* Scanning vs parsing
* Derivations
    * Leftmost vs rightmost
* Precedence
    * PEMDAS
* Ambiguity
    * match each else with closest if
    * could enforce priority for rules but then you need to respect the priority
* Parsing: the big picture
    * IR intermediate representation
* Top-down versus bottom-up parsers
    * topdown: LL 
        * first L : left-to-right reading of the input
        * second L : left-most derivation
    * bottomup: LR
        * R: right-most derivation
* Example
    * Look ahead to avoid backtracking
    * LL(1)
        * Lookahead
* Left-recursion
    * Top-down parsers cannot handle left-recrussion in a grammar
* How much lookahead is needed
* Predictive parsing
* Left-factoring
* Example
    * Now selection only requires a single LL(1)
* Generality
* Recursive descent parsing
* LL(1)-parsing:
    1. nonterminal A -> parser A()
    2. token T -> parser eat(t)
    3. RHS At -> A(); eat(t)
        * At is a sequence
        * A(); eat(t) is a sequence
* Recursive descent parsing
* Nullable
* First
* Follow
* LL(1) grammars
* LL(1) parse table construction
* LL(1) grammar
## 4/7/2023 Week 1 Friday Dis 1
* CS132 Compilers
* OH Mon 4-6pm Boelter 3256S-A
* LL1 Academy http://l1academy.cs.ucla.edu
* Homework Submission Guidelines
    * CS132 Framework (a tar file you can find on BruinLearn)
    * Read the instructions carefully and start early
* Homework 1 = Scanner + Parser
* What are the tokens in hw1
* Treat whole thing as a token
    * tokens are terminal symbols
* How do we recognize them in the code
* Finite Automata
* DFA vs NFA
* Regular Expression to NFA
* NFA to DFA
* How did you know what numbers to put in the NFA?
* Write the coda for the DFA in Java
    * Don't use shortcuts
    * Write DFA
* HW1: Scanner + Parser
* First(A), Follow(A), Nullable(A)
    * Ask about first examples?
* A Basic Structure of a Recursive Descent Parser
## 4/11/2023 Week 2 Tuesday Lec 3
* Java Compiler Compiler
    * "Lex and Yacc for Java"
    * Based on LL(k) rather than LALR(1)
* JavaCC input format
* Generating a parser with JavaCC
* The Visitor Pattern
    * Gamma, Helm, Johnson, Vlissides: Design Patterns, 1995
* Sneak Preview
* First Approach: Instanceof and Type Casts
* Second Approach: Dedicated Methods
* Third Approach: The Visitor Pattern
* Double dispatch
* Comparison
* Visitors Summary
* Java Tree Builder
    * JTB is a frontend for Java Compiler Compiler
* Using JTB
* Example (simplified)
## 4/13/2023 Week 2 Thursday Lec 4
* Typecheck
    * Minijava -> {true, false}
        * true then terminate with a type
        * false throw an exception
    * e ::= true | false | !e | c | e + e | e ? e : e
        * boolean constant
    * t ::= boolean | int
    * 5 + 7 ok
    * 5 + false X
    * true ? 5 : 7 ok
    * 9 ? 5 : 7 X
    * true ? 5: false X
    *       + (int)
    *     5   7
    *    int int
    * trees for operations
    * not that ? needs same types for right of ?
* Rule
    * Hypothesis 1 ... Hypothesis n / Conclusion
    * (H_1 \and ... \and H_n) => C
* Judgement
    * e : t
        * expression e has type t
* Rule
    * e_1:t e_2:t / r(...e_1 ... e_2 ...): t
    * false: boolean
    * true: boolean
    * r e: boolean / r !e: boolean
    * they add a sideways T before rules (I call r)
    * r c : int
    * re_1 : int re_2: int / re_1+e_2:int
    * re_1 : boolean  re_2: t_2  re_3: t_3  / e_1 ? e_2 : e_3
        * t_2 = t_3
        * (e_1 ? e_2 : e_3) : t_2
     * class TypeChecker extends DepthFirstVisitor {
        * String visit (IntConst n) {
            * return "int";
        * }
        * // f_0: left subtree; f_2: right subtree
        * String visit (Plus n) {
            * String t_0 = n.f_0.accept(this); // Step 1
            * String t_2 = n.f_2.accept(this); // Step 1
            * if (t_0 == "int" and t_2 == "int") { // Step 2
                * return "int"; // step 3
            * } else {
                * throw new Exception(); // step 3
            * }

        * }
     * }
* s ::= System.out.println(e); | if (e) s else s | while (e) s | x = e;
    * re:int / r System.out.println(e)
    * re: boolean rs_1 rs_2 / r if (e) s_1 else s_2
    * re: boolean rs / r while(e) s
    * e ::= ... | x
* Type environment (type checking people) = symbol table (compiler people)
    * A:
    * Name | Type
    * x | boolean
    * y | int
    * Judgement: Ar e: t Ar s
        * put As in every rule
    * Arx: t (A(x) = t)
    * A(x)=t_x Ar e: t_e / Ar x=e;
        * t_x = t_e
* Arrays
    * e ::= ... | new int[e] | e.length | e[e]
    * s ::= ... | x[e] = e; 
    * Ar e: int / Ar new int[e] : int[]
    * Ar e: int[] / Ar e.length: int
    * Ar e_1: int[]  Are_2: int / A r e_1[e_2] : int
    * A(x) = int[] Are_2: int Are_3: int / Ar x[e_2] = e_3
    * Class A {
        * int A;
        * void A (int A) {
            * int A; // this and above must be differnet
        * }
    * }
    * classnames, field names, method names are in different namespaces but local variables and parameters aren't
    * Build A
        * fields, parameters, local variables (in this order)
            * check that local variables are different from parameters
        * lookup from bottom to top
    * What happens if same name but different type?
        * doesn't matter, no same name for same namespaces
## 4/14/2023 Week 2 Friday Dis 2
* Start early
* Outline
* Java Inheriting Methods from Parent Class
* Overriding in Java
* Overloading in Java
* Generics in Java
* Generic Class/Interface
* Design Patterns in Software Engineering
* Visitor Pattern
* Visitor Pattern in JTB
* (Recommended) Using an IDE
* How to get started using the MiniJava Parser
* But How???
    * Override the visit methods
* Demo for Implementing an Instruction Counter
* Symbol Table
* Scopes
* In case you are bored
* Recommended Reading
## 4/20/2023 Week 3 Thursday Lec 6
* Sparrow
    * No classes, no fields 
    * Functions, local variables, labels and jumps
* (Program) p ::== F_1 ... F_m
* (FunDecl) F ::= func f(id_1 ... id_f) b
* (Block) b ::= i_1 ... i_n return id
* (Instruction) i ::= l: | id = c | id = @f | id = id + id | id = id - id | id = id * id | id = id < id | id = [id + c] | [id + c] = id | id = id | id = alloc (id) | print(id) | error(s) | goto l | if 0 id goto l | id = call id(id ... id)
    * c is integer literal
    * not a local variable
    * integers, heap values, functions are the value types allowed
* Values of Sparrow
    * integers c
    * heap addresses with offsets (a, c)
    * function names f
        * no bounds on sizes of integers, heap addresses, functions
* why did he do java Main s < benchmarks/Factorial.sparrow??? Also java Main check-s
* Semantics
    * Program state: (p, H, b^{\dot}, E, b)
        * p is program
        * H is the heap, gotos can go only within same function
        * b^{\dot} is the whole block of current function
        * E is envrionment (A is a type environment), means map from ids to values
        * b is executing next (is a block)
        * (p, H, b^{\dot}, E, b) -> (p, H', b^{\dot'}, E', b')
    * Execution: state_1 -> state_2 -> ... -> state_i -> ...
* (p, H, b^{\dot}, E, l: b) -> (p, H, b^\{dot}, E, b)
    * (p, H, b^{\dot}, E, id = c b) -> (p, H, b^\{dot}, E \dot [id |-> c], b)
        * [id |-> c] takes preference over E
* (p, H, b^{\dot}, E, id = @f b) -> (p, H, b^\{dot}, E\dot [id |-> f], b )
* (p, H, b^{\dot}, E, id = id_1 + id_2 b) -> (p, H, b^{\dot}, E \dot [id |-> (c_1 + c_2)], b) 
    * if E(id_1) = c_1 \and E(id_2) = c_2
* (p, H, b^{\dot}, E, id = id_1 + id_2 b) -> (p, H, b^{\dot}, E \dot [id |-> (a_1, c_1 + c_2)], b)
    * if E(id_1) = (a_1, c_1) \and E(id_2) = c_2
        * what is a_1?????
* (p, H, b^{\dot}, E, id = id_1 < id_2 b) -> (p, H, b^{\dot}, E \dot [id |-> 1], b)
    * if E(id_1) = c_1 \and E(id_2) = c_2 \and c_1 < c_2
* (p, H, b^\{dot}, E, id = [id_1 + c] b) -> (p, H, b^\{dot}, E \dot [id |-> H(a_1)(c_1 + c)], b)
    * if E(id_1) = (a_1, c_1)
        * (c_1 + c) \in dom(H(a_1))
* H in (p, H, ...) is a map from a to a tuple of values
    * refer to picture on phone
* (p, H, b^{\dot}, E, [id_1 + c] = id b) -> (p, H \dot [a_1 |-> t], b^\{dot}, E, b)
    * if E(id_1) = (a_1, c_1)
        * (c_1 + c) \in dom(H(a_1))
        * t = H(a_1) \dot [(c_1 + c_2) |-> E(id)]
* (p, H, b^{\dot}, E, id = alloc(id_1) b) -> (p,H\cdot [a |-> t], b^{\dot}, E \cdot [id |-> (a, 0) ], b)
    * a \not \in dom(H)
    * E(id_1) = c \and c >= 0 \land c divisible by 4
    * t = 0 |-> 0, 4 -|-> 0 ... c-4 |-> 0
* (p, H, b^{\dot}, E, if 0 id goto l b) |-> (p, H, b^\{dot}, E, b')
    * if E(id) = 0 
        * find (b^\{dot}, l) = b'
* (p, H, b^{\dot}, E, id = call id_0(id_1 ... id_f) b) |-> (p, H, b', [id_1^' |-> , ..., id_f^' |-> ], b')
    * |->* (p, H', b', E', return id')
    * id_1 ... id_f are actual paramters in id = call id_0 () 
    * E(id_0) = f
        * p contains func f (id_1^' ... id_f^') b'
            * these id_1^' ... id_f^' are formal parameters
    * |-> (p, H', b^{\dot}, E \dot [id |-> E'[id']], b)
## 4/21/2023 Week 3 Friday Dis 3
* Start early
    * Start HW2 now
* Outline
* Symbol Table
* What data structure though?
* Scope
* Handling Scopes
* Example Code from the Textbook
* Make your own Typecheck.java 
    * Use it instead
    * LinkedLists only include types for symbol tables
    * Code is in Chapter
    * type("")
    * Don't have to download JTB
* Type Rules
* Some type of data structure to keep track of subtypings
* In case you are stuck...
* read slides for last part
* ASK PROF OR TA OR MICHAEL ABOUT CREATING A STATIC CLASS AND USING THAT TO STORE ALL CONTENTS????
## 5/5/2023 Week 5 Friday Dis 5
* Outline
* Sparrow - Program State
* Semantic Rules for Sparrow
* Running the Sparrow Interpreter
    * use first four
        * s
        * s input
        * s verbose
        * check-s
* From MiniJava to Sparrow
* MiniJava Program Semantics
* MiniJava vs Sparrow
* Arrays
* Array out of bound error
    * Why don't we just check that at compile time?
* Sparrow: So how should we implement an object?
    * Each object is allocated on the Heap, the memory layout looks like this
* Objects - Basic Ver.
* Objects - Advanced Ver.
* Use sparrow package 
## 5/12/2023 Week 6 Friday Dis 6
* Liveness analysis is on final 
## 5/19/2023 Week 7 Friday Dis 7
* Source code of Sparrow syntax tree
* Live Range Analysis
* Linear Scan register Allocation
* Possible Optimization Ideas
# 5/26/2023 Week 8 Friday Dis 8
* Final similar to quizzes
* Not a valid sparrow 5 program
    * Turn into it
* ASK ABOUT SCC ANALYSIS???
## 6/9/2023 Week 10 Friday Dis 10
* How to compile lambda questions