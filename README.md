# udacity_testing_javascript
```javascript
  var this = function(){
    console.log('testing')
};
```

  - The entire spec for a particular javascript file is basically one or more
    describe functions.
  - `describe` functions in Jasmine take a string and a callback.
    - The entirety of the spec file can be contained within this callback.

    ```javascript
    describe("Player", function() {
        var player;
        var song;

        beforeEach(function() {
            player = new Player();
            song = new Song();
            });

        it("should be able to play a Song", function() {
            player.play(song);
            expect(player.currentlyPlayingSong).toEqual(song);

            //demonstrates use of custom matcher
            expect(player).toBePlaying(song);
            });
        });
```
  - `it` similarly takes a string and a callback

- Add files to SpecRunner.html to ensure that they're run in the browser

##Testing Async Functions
  - You can use the `done()` method to indicate to your test when an
    asynchronous function has completed

```javascript
describe('Async Address Book', function() {
  var addressBook = new AddressBook();
```

- In the `beforeEach` function, you pass the `done` function as the argument in
its callback. Remember, take special note of the case where if you pass in the
`done` function as an argument, you **must** also call it (otherwise things break!). 

```javascript
  beforeEach(function(done) {
    addressBook.getInitialContacts(function() {
      done();
    });
  });
```

- Then you need to signal to Jasmine which of your specs relied upon `done`.
This is done by calling `done()` after your expectation. Don't forget to pass
it in as an argument.

```javascript
  beforeEach(function(done) {
  it('should grab initial contacts', function() {

    expect(addressBook.initialComplete).toBe(true);
    done();
  });
});
```
