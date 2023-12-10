# MailHedgehog gounit

Testing helper for MailHedgehog package. Can be reused in any other app/package.

Contains a set of helpers to quicker assert conditions.

## Usage

`(*gounit.T)(t).AssertEqualsString("expected", "value")`

```go
package main

import (
    "github.com/mailhedgehog/gounit"
    "testing"
)

func TestToSMTPMail(t *testing.T) {
    smtpMessage := &SMTPMessage{
        Helo: "test-X510",
        From: "from@example.com",
        To: []string{
            "joe@example.net",
            "cc@example.com",
        },
        Data: "",
    }

    smtpMail, err := smtpMessage.ToSMTPMail("foo-bar")
    (*gounit.T)(t).AssertNotError(err)
    (*gounit.T)(t).AssertEqualsString("foo-bar", string(smtpMail.ID))
    (*gounit.T)(t).AssertEqualsString(smtpMessage.From, smtpMail.From.Address())
    for i, to := range smtpMessage.To {
        (*gounit.T)(t).AssertEqualsString(to, smtpMail.To[i].Address())
    }
    // nil because content empty
    (*gounit.T)(t).AssertNil(smtpMail.Email)
}
```

## Development

```shell
go mod tidy
go mod verify
go mod vendor
```

## Credits

- [![Think Studio](https://yaroslawww.github.io/images/sponsors/packages/logo-think-studio.png)](https://think.studio/)
