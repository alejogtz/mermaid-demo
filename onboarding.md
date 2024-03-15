
### Onboarding process

```mermaid
stateDiagram
    [*] --> waiting_send_link

    waiting_send_otp --> otp_verifying : send_code
    waiting_identity_data --> waiting_address_data : save_data
    otp_verified --> waiting_identity_data : on_enter callback
    otp_verifying --> otp_verified : verify
    otp_verifying --> otp_verify_failed : verify
    otp_verifying --> otp_verify_failed : send_code
    otp_verify_failed --> onboarding_failed : on_enter hook
    onboarding_failed --> [*]
    otp_verifying --> waiting_identity_data : skip_otp
    reviewing --> link_sent : send_link
    reviewing --> link_sent : cancel_review
    waiting_send_link --> link_sent : send_link
    link_sent --> waiting_send_otp : save_data
    link_sent --> reviewing : review
    waiting_call_time --> onboarding_completed : save_data
    waiting_address_data --> waiting_call_time : save_data
    waiting_address_data --> waiting_incomes_data : save_data
    waiting_incomes_data --> waiting_call_time : save_data


    onboarding_completed --> [*]
```