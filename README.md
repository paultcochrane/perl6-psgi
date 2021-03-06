# PSGI for Perl 6

## Introduction

A helper library for creating PSGI-compliant frameworks in Perl 6.

Currently provides the encode-psgi-response() subroutine, which takes
a PSGI-response from an application, and parses it into a CGI or HTTP
response (in either Str or Buf format, depending on the Body contents.)

## Usage

```perl
  use PSGI;

  ## Using a traditional PSGI response array.
  ## Headers are an Array of Pairs.
  ## Body is an Array of Str or Buf.
  my $status   = 200;
  my $headers  = ['Content-Type'=>'text/plain'];
  my $body     = ["Hello world"];
  my @response = [ $status, $headers, $body ];
  my $string = encode-psgi-response(@response);
  ##
  ##   Status: 200 OK
  ##   Content-Type: text/plain
  ##
  ##   Hello world
  ##

  ## Passing the elements individually.
  ## Also, this time, we want to use NPH output.
  $string = encode-psgi-response($status, $headers, $body, :nph);
  ##
  ##   HTTP/1.0 200 OK
  ##   Content-Type: text/plain
  ##
  ##   Hello world
  ##

  ## Now an example using a Hash for headers, and a singleton
  ## for the body.
  my %headers = {
    Content-Type => 'text/plain',
  };
  my $body-text = "Hello world";
  $string = encode-psgi-response($code, %headers, $body-text);
  ##
  ## Same output as first example
  ##

```

See the tests for further examples.

## Author 

Timothy Totten, supernovus on #perl6, https://github.com/supernovus/

## License

Artistic License 2.0

