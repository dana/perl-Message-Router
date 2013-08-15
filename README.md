# NAME

Message::Router - Fast, simple message routing

# SYNOPSIS

    use Message::Router qw(mroute mroute_config);

    sub main::handler1 {
        my %args = @_;
        #gets:
        # $args{message}
        # $args{route}
        # $args{routes}
        # $args{forward}
        print "$args{message}->{this}\n"; #from the transform
        print "$args{forward}->{x}\n";    #from the specific forward
    }

    mroute_config({
        routes => [
            {   match => {
                    a => 'b',
                },
                forwards => [
                    {   handler => 'main::handler1',
                        x => 'y',
                    },
                ],
                transform => {
                    this => 'that',
                },
            }
        ],
    });
    mroute({a => 'b'}); #prints 'that', and then 'y', per the handler1 sub

# DESCRIPTION

This library allows fast, flexible and general message routing.

# FUNCTION

## mroute\_config($config);

The config used by all mroute calls

## mroute($message);

Pass $message through the config; this will emit zero or more callbacks.

# TODO

A config validator.
Short-circuiting
More flexible match and transform configuration forms

# BUGS

None known.

# COPYRIGHT

Copyright (c) 2012, 2013 Dana M. Diederich. All Rights Reserved.

# AUTHOR

Dana M. Diederich <diederich@gmail.com>
