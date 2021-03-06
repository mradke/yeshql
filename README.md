# YeshQL

[YesQL](https://github.com/krisajenkins/yesql)-style SQL database abstraction.

YeshQL implements quasiquoters that allow the programmer to write SQL queries
in SQL, and embed these into Haskell programs using quasi-quotation. YeshQL
takes care of generating suitable functions that will run the SQL queries
against a database driver, and marshal values between Haskell and SQL.

In order to do this properly, YeshQL extends SQL syntax with type annotations
and function names; other than that, it is perfectly ignorant about the SQL
syntax itself. See the [YesQL
Readme](https://github.com/krisajenkins/yesql/blob/master/README.md) for the
full rationale - Haskell and Clojure are sufficiently different languages, but
the reasoning behind YesQL applies to YeshQL almost unchanged.

The project is split up into a core library, `yesh-core`, and separate
libraries for the supported backends.

## Installation

Use [stack](http://haskellstack.org/) or [cabal](http://haskell.org/cabal/) to
install. Nothing extraordinary here.

## Usage

In short:

    {-#LANGUAGE QuasiQuotes #-}
    import MyProject.DatabaseConnection (withDB)
    import Database.HDBC
    import Database.YeshQL.HDBC

    [yesh|
      -- name:getUser :: (String)
      -- :userID :: Int
      SELECT username FROM users WHERE id = :userID
    |] 

    main = withDB $ \conn -> do
      username <- getUser 1 conn
      putStrLn username

Please refer to the Haddock documentation for further usage details.

## Bugs

Probably. The project is hosted at https://github.com/tdammers/yeshql, feel
free to comment there or send a message to tdammers@gmail.com if you find any.

## Something about the name

YeshQL is rather heavily inspired by YesQL, so it makes sense to blatantly
steal most of the name. Throwing in an "H" for good measure (this being Haskell
and all) makes it sound like Sean Connery, which automatically increases
aweshomenesh, so that'sh what we'll roll with.

## License / Copying

YeshQL is Free Software and provided as-is. Please see the enclosed LICENSE
file for details.
