---
layout: default
title: ProgLang
---

~~~
This example is made by Bernhard K. Aichernig and Andreas Kerschbaumer 
#******************************************************
~~~
###ast.vdmsl

{% raw %}
~~~

module AST
exports all
definitions
types
  Program :: decls : seq of Declaration
  Declaration :: id  : Identifier
  Identifier = seq1 of char;
  Type = <BoolType> | <IntType> ;
  Value = BoolVal | IntVal;
  BoolVal :: val : bool;
  IntVal :: val : int;
  Stmt = BlockStmt | AssignStmt | CondStmt | ForStmt | RepeatStmt;
  BlockStmt :: decls : seq of Declaration
  AssignStmt :: lhs : Variable
  Variable :: id : Identifier;
  Expr = BinaryExpr | Value | Variable;
  BinaryExpr :: lhs : Expr
  Operator = <Add> | <Sub> | <Div> | <Mul> | <Lt> | <Gt> | <Eq> | <And> | <Or>;
  CondStmt :: guard  : Expr
  ForStmt :: start : AssignStmt
  RepeatStmt :: repeat : Stmt
end AST

~~~{% endraw %}

###dynsem.vdmsl

{% raw %}
~~~

module DYNSEM
imports
exports all
definitions
types
  DynEnv = map AST`Identifier to AST`Value;
functions
  EvalProgram : AST`Program -> DynEnv
  EvalDeclarations : seq of AST`Declaration -> DynEnv

  EvalStmt : AST`Stmt * DynEnv -> DynEnv
  EvalBlockStmt : AST`BlockStmt * DynEnv -> DynEnv
  EvalStmts : seq of AST`Stmt * DynEnv -> DynEnv
  LenStmt: seq of AST`Stmt * DynEnv -> nat
  EvalAssignStmt : AST`AssignStmt * DynEnv -> DynEnv
  EvalCondStmt : AST`CondStmt * DynEnv -> DynEnv
  EvalRepeatStmt : AST`RepeatStmt * DynEnv -> DynEnv
  EvalForStmt : AST`ForStmt * DynEnv -> DynEnv
  EvalForLoop : AST`Variable * AST`Value * AST`Stmt * DynEnv -> DynEnv
  LoopParInc: AST`Variable * AST`Value * AST`Stmt * DynEnv -> nat
  EvalExpr : AST`Expr * DynEnv -> AST`Value
  EvalBinaryExpr : AST`BinaryExpr * DynEnv -> AST`Value
end DYNSEM

~~~{% endraw %}

###statsem.vdmsl

{% raw %}
~~~

module STATSEM
imports from AST all
exports all
definitions
types
  StatEnv = map AST`Identifier to AST`Type;
functions
  wf_Program : AST`Program -> bool
wf_Declarations : seq of AST`Declaration -> bool
get_Declarations : seq of AST`Declaration -> StatEnv
wf_Stmt : AST`Stmt * StatEnv -> bool
wf_BlockStmt : AST`BlockStmt * StatEnv -> bool
wf_Stmts : seq of AST`Stmt * StatEnv -> bool
wf_AssignStmt : AST`AssignStmt * StatEnv -> bool * [AST`Type]
wf_CondStmt : AST`CondStmt * StatEnv -> bool
wf_RepeatStmt : AST`RepeatStmt * StatEnv -> bool
wf_ForStmt : AST`ForStmt * StatEnv -> bool
wf_Expr : AST`Expr * StatEnv -> bool * [AST`Type]
wf_Variable : AST`Variable * StatEnv -> bool * [AST`Type]
wf_BinaryExpr : AST`BinaryExpr * StatEnv -> bool * [AST`Type]
end STATSEM

~~~{% endraw %}

###Test.vdmsl

{% raw %}
~~~

module Test
imports 
exports all
values 
  binexpr: AST`Expr = 
RunTypeCheck: () -> bool * [AST`Type]
RunEval: () -> AST`Value
end Test

~~~{% endraw %}
