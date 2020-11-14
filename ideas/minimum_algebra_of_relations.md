% Minimum Algebra of Relations

The objective of this text is to present ways to represent a 
relation that is complete, ie, covers all of the possible relations.

Well, not all of the relations, only the finite ones, for simplicity 
sake.

# Type System of Relations

    tR ::= t <- t

    t ::= 1
    t ::= t x t
    t ::= t + t

Basically finite algebraic data type.

# Complete Algebra of Relations (CAR)

    R,S ::=
    RxS , < , > ,
    R+S , [ , ] ,
    R.S , ⊥ , T

All this operators and elements can be used to create any relation 
of the types we are worried about.

## Types

    R : B <- A ∧ S : D <- C <=> RxS : BxD <- AxC
    > : AxA <- A
    < : A <- AxA

    R : B <- A ∧ S : D <- C <=> R+S : B+D <- A+C
    ] : A+A <- A
    [ : A <- A+A

    R : C <- B ∧ S : B <- A <=> R.S : C <- A
    ⊥ : 1 <- 1
    T : 1 <- 1

The bottom and the top are used only from 1 to 1, because we can 
define the other types with induction in the types. But we will 
use the same simbol for all the types, for simplicity.

## Behaviour

    (c,d) (RxS) (a,b) <=> c R a ∧ d S b
    (a,a) > a
    a < (a,a)

    b (R+S) a <=> b (i1 . R . i1º) a ∨ b (i2 . S . i2º) a
    b ] a <=> b i1 a ∨ b i2 a
    a [ b <=> b i1 a ∨ b i2 a

    c (R.S) a <=> ∃b:: c R b ∧ b S a
    a ⊥ b <=> FALSE
    a T b <=> TRUE

# Composition

The composition given by _._, can be very helpfull for readability,
but for asking about properties of that relation is not so great,
for example if we want to now if 
    R ⊆ S
or
    R = S
then the composition is our enemy.

# No Composition

We are going to try to represent the algebra we were talking about
but without composition.

## First Try (FT)

    F,G ::= 
    <FxG) , (FxG> ,
    [F+G) , (F+G] ,
    ⊥     , T

To transform FT to CAR is simple, but when trying to transform CAR to FT
we can encounter the following problem.
    >.] and [.<
cannot be represented by FT.

Why??

Because there is no R and S, such that 
    (R x S> = >.]

Even if we upgraded with >.], we would have the same problem with
    >.].]

## Second Try (ST)
    
    F,G ::= 
    n<FxG) , (FxG>n ,
    [F+G) , (F+G] ,
    ⊥     , T
    ∀n∈N0

### id

    (id: 1<-1) := T
    (id: AxB<-AxB) := < (idxT> x (Txid> ) = ( <idxT) x <Txid) >
    (id: A+B<-A+B) := [ (id+⊥] + (⊥+id] ) = ( [id+⊥) + [⊥+id) ]

### ST -> CAR

    ⊥ := ⊥
    T := T

    0<FxG) := < . (FxG)
    (n+1)<FxG) := [ . n<FxG)
    (FxG>0 := (FxG) . >
    (FxG>(n+1) := (FxG>n . ]

    [F+G) := [ . (FxG)
    (F+G] := (FxG) . ]

### CAR -> ST

    ⊥ := ⊥
    T := T
    
    RxS := < (RxT> x (TxS> ) = ( <RxT) x <TxS) >
    > := (id x id>
    < := <id x id)

    R+S := [ (R+⊥] + (⊥+S] ) = ( [R+⊥) + [⊥+S) ]
    ] := (id + id]
    [ := [id + id)

#### R.S = ?

The composition we need more induction.

    ⊥.R = ⊥
    R.⊥ = ⊥
    T.R = R
    R.T = R

    n<RxS) . m<QxK) := 
    n<RxS) . (QxK>m := R.Q ∩ S.K
    n<RxS) . [Q+K)  := 
    n<RxS) . (Q+K]  := ⊥
    (RxS>n . m<QxK) := 
    (RxS>n . (QxK>m := 
    (RxS>n . [Q+K)  := 
    (RxS>n . (Q+K]  := 
    [R+S)  . m<QxK) := 
    [R+S)  . (QxK>m := ⊥
    [R+S)  . [Q+K)  := 
    [R+S)  . (Q+K]  := R.Q ∪ S.K
    (R+S]  . m<QxK) := 
    (R+S]  . (QxK>m := 
    (R+S]  . [Q+K)  := 
    (R+S]  . (Q+K]  := 
