!SLIDE 
# Dollar Spec
## ($spec)

#### Jim Benton
#### @automach

!SLIDE bullets incremental
# What is it?
* A tiny experimental JavaScript spec framework

!SLIDE bullets incremental
# Features
* Small, hackable codebase
* Favors explicitness over magic
* Nested describe blocks
* Before/after blocks
* Easy to extend with new expectations

!SLIDE bullets incremental
# What does it look like?

!SLIDE
    @@@ javascript
    var add = function(a, b) {
      return a + b;
    };
    
    $spec.describe('addition', function(spec) {

      spec.it('adds numbers', function(expect) {
        expect(add(2,2)).to.equal(4);
      });

    });

!SLIDE bullets
# Supported expectations
 * equal
 * beA
 * beNull
 * beUndefined
 * change / change by
 * raiseError

!SLIDE
## Negating an expectation
    @@@ javascript
    
    expect(4).to.equal(4);
    
    expect(4).to.not().equal(5);

!SLIDE
# Defining a new expectation

!SLIDE
    @@@ javascript
    expect(2).to.beLessThan(5);

!SLIDE smaller
    @@@ javascript 
    // expect(2).to.beLessThan(5);
    
    $spec.verb('beLessThan', function(expected) {
      this.set('matcher', 'beLessThan');
      this.set('expected', expected);
      return this;
    });

!SLIDE smaller
    @@@ javascript 
    // expect(2).to.beLessThan(5);
    
    $spec.matcher('beLessThan', function(result) {

      result.failure = "Expected " + String(this.actual) + 
        " to be less than " + String(this.expected);

      result.negatedFailure = "Expected " + String(this.actual) +
        " to not be less than " + String(this.expected);
  
      return this.actual < this.expected;
    });
    

!SLIDE
    @@@ javascript
    expect(someValue).to.beBetween(6).and(90);
    
!SLIDE
    @@@ javascript
    var count = 400;

    expect(function() {
      count += 1;
    }).to.change(function() {
      return count;
    });
    
!SLIDE
    @@@ javascript
    var count = 400;

    expect(function() {
      count += 1;
    }).to.change(function() {
      return count;
    }).by(1);

!SLIDE
# Other grammer options

!SLIDE
    @@@ javascript
    expect(1).to.equal(1);
    expect(1).to.not().equal(2);

    // possibilities...

    expect(1).to.equal(1);
    expect(1).toNot().equal(2);

    verify(1).equals(1);
    verify(1).doesNot().equal(2);

!SLIDE
# But I need to run tests in multiple browsers simultaneously

!SLIDE bullets incremental
# Diligence
* Small server written in express/Node.js
* Runs tests in multiple browsers
* Prints results to the console
* Provides useful stacktraces*

!SLIDE
# Demo

!SLIDE bullets
# To Do
* More browser support
* Create a npm package for simple installation
* Provide a simple project setup script
* Use fs.watchFile to detect file changes

!SLIDE bullets
# Alternatives

### (That are more complete and stable)

* Jasmine
* QUnit
* Many more...

!SLIDE
# Thanks
## github.com/jim/dollar_spec
## github.com/jim/diligence

## @automach
## jim@autonomousmachine.com