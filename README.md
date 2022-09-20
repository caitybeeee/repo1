# repo1
this is a test

when HTTP_REQUEST {
    set foo 0
    if { [HTTP::uri] starts_with "/foo/" } {
        set foo 1
        pool my_pool
    }
}
when SERVER_CONNECTED {
    if { $foo } {
        SSL::profile /ROUTEDOMAIN1/serverssl-mypool
    }
}
when LB_FAILED {
    log local0. "DEBUG2: event info: [event info]"
    log local0. "DEBUG2.1: lb info: [LB::server]"
}
