# TODO

- [ ] Dont use public fields, se private properties with get private set and explain it for non c# devs
- [X] Missing ATC overview (remove from summary?)
- [X] Traffix typo
- [X] int newAltitude typehint
- [X] Change aggregateId to modelId
- [X] On the "About the SimSuite software" slide, Traffic is spelled wrong. I'd also recommend expanding the SimTarget description to be "Traffic Generation".
- [X] Approach controllers don't control the plane during landings (tower controllers do that). Approach controllers handle the final descent and approach to the airport. Once the plane is lined up with the runway, it is handed off to tower.
- [X] The SimVox Communication slide has a typo, missing the word "be" in between "can" and "used".
- [X] On the "New Requirements" slide, I would modify the 2nd bullet point a bit to say "When a student fails a scenario, the instructor can rewind the recorded scenario to a chosen point in time to allow the student to retry without the need to start from the beginning." (I think this language highlights the benefits of a timestamped event stream a bit better.)
- [X] On the "Persisting Events" slide, missing a comma or the word "and" after the word "stack".
- [X] On the "Problems with event sourcing" slide, "replying" should be "replaying".
- [ ] I think we talked about this a little already, but were you planning to talk about other common uses of event sourcing, such as bank ledgers, ecommerce, etc?
- [ ] How would you do this slide, have a better answer myself

- [ ] On the example model code slide, should the altitude field be private, with a public getter? (I would probably use a property with "private set", like you did here: https://bitbucket.org/bglassman/simsuite/src/82c16c0e1e86f1c6467e5783f7325a66dfb983b4/Model/State/AircraftState.cs?at=master&fileviewer=file-view-default#AircraftState.cs-8 )
- [ ] This is not really relevant to your presentation, but another way to implement the ReleaseEvents() method would be something like:
    List<ModelChangedEvent> releasedEvents = new List<ModelChangedEvent>(events);
    events.Clear();
    return releasedEvents;
    I'm not sure which of these is more performant (I have a hunch your way might be better, since it doesn't involve copying the list) ... might be something I'll do some benchmarking on since this method will be called frequently.
- [ ] Also on the topic of performance, (and also not really relevant to the presentation,) I wonder if there might be a better way for the Apply() method to determine which event-class-specific Apply*() method to delegate to, instead of using a switch statement with string comparison. I was thinking maybe each Aggregate would maintain a static mapping of event types to a Func<T> that points to the associated Apply*() method. Let me know if you want me to write some example code for how that might look.
- [ ] When reconstituting models, should the ReconstituteFromEvents() method sort the events by version, or at least validate that each event in the list has a higher version than the one before? I'm not sure where that responsibility should lie.
