## Jest

Zero-configuration testing platform for javascript.

### Snapshot Testing

Jest supports snapshot testing. Snapshot testing (a.k.a Gold Master Testing)
allows you to take snapshots of data that will cause a failing test if the data
changes between subsequent test runs.

This is mainly used for testing changes in UI (html), but can also be used for
testing redux reducer (json) because of their pure nature.

> Snapshots work because of developer trust!

#### Usage

See: [Jest - Snapshot Testing][1]  

### Useful Links

#### Jest

[Jest](https://facebook.github.io/jest/)  
[Testing React components with Jest and Enzyme](https://hackernoon.com/testing-react-components-with-jest-and-enzyme-41d592c174f)  
[adriantoine/enzyme-to-json](https://github.com/adriantoine/enzyme-to-json) - Use Enzyme shallow render w/ Snapshots  

#### Snapshots Testing

[Jest - Snapshot Testing][1]
[Testing with Jest Snapshots: First Impressions](https://benmccormick.org/2016/09/19/testing-with-jest-snapshots-first-impressions/)  
[Snapshot Testing: Use With Care](http://randycoulman.com/blog/2016/09/06/snapshot-testing-use-with-care/)  
[Gold Master Testing](https://codeclimate.com/blog/gold-master-testing/)  
[How we landed on Jest snapshot testing for JavaScript](https://blog.grommet.io/post/2016/09/01/how-we-landed-on-jest-snapshot-testing-for-javascript)  
[Thoughts on Jest Snapshots](http://blog.scottlogic.com/2017/09/01/thoughts-on-jest-snapshots.html)  
[Jest 14.0: React Tree Snapshot Testing](https://facebook.github.io/jest/blog/2016/07/27/jest-14.html) - Why use snapshots?


[1]: https://facebook.github.io/jest/docs/en/snapshot-testing.html
